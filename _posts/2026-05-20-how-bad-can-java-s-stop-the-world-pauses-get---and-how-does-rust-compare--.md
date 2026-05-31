---
category: Technical
date: 2026-05-20
layout: post
title: How Bad Can Java's Stop-the-World Pauses Get? (And How Does Rust Compare?)
updated: 2026-05-20
---

I recently read [(How bad can Python stop-the-world pauses get?)](https://lemire.me/blog/2026/02/15/how-bad-can-python-stop-the-world-pauses-get/). It describes a way to demonstrate how Python's garbage collector will pause the application in order to claim back the memory. There is no deterministic way to know when this will trigger. Hence, this can lead to unexpected latency in the application. It gives a simple Python program to demonstrate it.

I wanted to understand how this would work out in a Java program. I wanted to compare it with a Rust program execution where there is no garbage collector.

For this experiment, I used the following Java version with the default G1 garbage collector.

```
openjdk version "26" 2026-03-17
OpenJDK Runtime Environment (build 26+35-2893)
OpenJDK 64-Bit Server VM (build 26+35-2893, mixed mode, sharing)
```

Here is the Java program

```java


import java.time.Duration;
import java.time.Instant;

class Node {

    private int value;
    private Node next;

    public Node() {
        this.next = null;
        this.value = 0;
    }

    public void addNext(Node node) {
        this.next = node;
    }

    public Node getNext() {
        return this.next;
    }

    public void setValue(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }
}



class StopTheWorld {

    public static Node createLinkedList(int limit) {
        Node headNode = new Node();
        headNode.setValue(0);
        Node current = headNode;

        for (int i = 0; i < limit; i++) {
            Node newNode = new Node();
            newNode.setValue(i);
            current.addNext(newNode);
            current = newNode;
        }

        return headNode;
    }

    public static void main(String[] args) {
        Instant start = Instant.now();
        Instant initStart = Instant.now();
        Node linkedList = createLinkedList(50_000_000);
        long initTime = Duration.between(initStart, Instant.now()).toNanos() / 1000;
        Instant oldStart = Instant.now();
        long delay = 0;
        long worstCase = 0;
        long createTime = 0;
        long worstCreateTime = 0;
        Instant loopStart = Instant.now();
        for (int i = 0; i < 1000000; i++) {
            Instant min_start = Instant.now();
            long value = Duration.between(oldStart, min_start).toNanos() / 1000;
            if (value > worstCase) {
                worstCase = value;
            }
            delay += value;
            Instant createStart = Instant.now();
            createLinkedList(1000);
            long thisCreateTime = Duration.between(createStart, Instant.now()).toNanos() / 1000;
            if (thisCreateTime > worstCreateTime) {
                worstCreateTime = thisCreateTime;
            }
            createTime += thisCreateTime;
            oldStart = min_start;
        }
        long loopTime = Duration.between(loopStart, Instant.now()).toNanos() / 1000;
        Instant end = Instant.now();
        Duration elapsed = Duration.between(start, end);
        System.out.println("Elapsed: " + elapsed.toMillis() + " ms");
        System.out.println("Initial 50M list create time: " + initTime + " µs");
        System.out.println("Total For Loop time (1M x 1K): " + loopTime + " µs");
        System.out.println("Total Delays between iteration: " + delay + " µs");
        System.out.println("Worst Gap is: " + worstCase + " µs");
        System.out.println("Total Create time: " + createTime + " µs");
        System.out.println("Worst Create time: " + worstCreateTime + " µs");
    }
}

```

Here is the output of the Java program.

```
➜  simple-programs java StopTheWorld
Elapsed: 7670 ms
Initial 50M list create time: 2622048 µs
Total For Loop time (1M x 1K): 5048015 µs
Total Delays between iteration: 4711094 µs
Worst Gap is: 565162 µs
Total Create time: 4568381 µs
Worst Create time: 565142 µs
```


For Rust, I used `rustc 1.93.0 (254b59607 2026-01-19)`. Here is the equivalent Rust program.

```rust
use std::time::Instant;

struct Node {
    value: i32,
    next: Option<Box<Node>>,
}

impl Node {
    fn new(value: i32) -> Self {
        Node { value, next: None }
    }
}

impl Drop for Node {
    fn drop(&mut self) {
        let mut current = self.next.take();
        while let Some(mut node) = current {
            current = node.next.take();
        }
    }
}

fn create_linked_list(limit: i32) -> Box<Node> {
    let mut head = Box::new(Node::new(0));
    let mut current: *mut Node = &mut *head;

    for i in 0..limit {
        let new_node = Box::new(Node::new(i));
        unsafe {
            (*current).next = Some(new_node);
            current = &mut **(*current).next.as_mut().unwrap();
        }
    }

    head
}

fn main() {
    let start = Instant::now();

    let init_start = Instant::now();
    let _linked_list = create_linked_list(50_000_000);
    let init_time = init_start.elapsed().as_micros();

    let mut old_start = Instant::now();
    let mut delay: u128 = 0;
    let mut worst_case: u128 = 0;
    let mut create_time: u128 = 0;
    let mut worst_create_time: u128 = 0;

    let loop_start = Instant::now();
    for _ in 0..1_000_000 {
        let min_start = Instant::now();
        let value = min_start.duration_since(old_start).as_micros();
        if value > worst_case {
            worst_case = value;
        }
        delay += value;
        let create_start = Instant::now();
        let _list = create_linked_list(1000);
        let this_create_time = create_start.elapsed().as_micros();
        if this_create_time > worst_create_time {
            worst_create_time = this_create_time;
        }
        create_time += this_create_time;
        old_start = min_start;
    }
    let loop_time = loop_start.elapsed().as_micros();

    let elapsed = start.elapsed();
    println!("Elapsed: {} ms", elapsed.as_millis());
    println!("Initial 50M list create time: {} µs", init_time);
    println!("Total For Loop time (1M x 1K): {} µs", loop_time);
    println!("Total Delays between iteration: {} µs", delay);
    println!("Worst Gap is: {} µs", worst_case);
    println!("Total Create time: {} µs", create_time);
    println!("Worst Create time: {} µs", worst_create_time);
}

```

Here is the output of the Rust program.

```
➜  simple-programs ./stop_the_world
Elapsed: 26915 ms
Initial 50M list create time: 1737040 µs
Total For Loop time (1M x 1K): 25178866 µs
Total Delays between iteration: 24577577 µs
Worst Gap is: 145 µs
Total Create time: 10964945 µs
Worst Create time: 90 µs
```

The code is trying to stress test the memory allocation. We are using a linked list for this experiment. We create one big 50 million nodes linked list and then 1 million small 1000 nodes linked lists. Here is the tabular output for comparison.

| Metrics                                                                          | Java      | Rust     |
| -------------------------------------------------------------------------------- | --------- | -------- |
| Program Execution Time                                                           | 7670 ms   | 26915 ms |
| Initial 50M node linked list creation time                                       | 2622 ms   | 1737 ms  |
| Total time for creating 1M 1k node linked list creation time (including delays)  | 5048 ms   | 25179 ms |
| Total delays between single 1k node linked list creations                        | 4711 ms   | 24578 ms |
| Worst Gap between the individual iteration                                       | 565162 µs | 145 µs   |
| Total time spent in just creating 1M of 1k node linked list (without gaps/delays) | 4568 ms   | 10965 ms |
| Max time spent in creating one single 1k node linked list (including gap)        | 565142 µs | 90 µs    |


On a high level, these results looked weird. My mental model was Rust is more of a systems programming language and hence should have been faster than Java across every metric. Here, we see that the Java program completed about 3.5x faster than Rust. Let's look into the following metrics and try to understand why that is happening:
- Total time for creating 1M 1k node linked list creation time (including delays)
	- This is the total loop time (1M x 1k). Here, Java is almost 5x faster than Rust.
	- The key here is, in every iteration, a 1k node linked list is formed and by the end of the iteration, that linked list has gone out of scope.
	- In the Rust world, the moment it goes out of scope, Rust deletes it. So, for Rust, every iteration = allocation + *any work after allocation* + delete.
	- In the Java world, there is only allocation and no deletion. Deletion is taken care by the GC at a later time. So, for Java, every iteration = allocation + *any work after allocation*. Hence, Java is much faster here.
- Total delays between single 1k node linked list creations
	- This is the total iteration delays. Here too, Java is 5x faster than Rust.
	- This makes sense given how every iteration differs in Rust world vs Java world. In Rust, the extra time goes toward deletion. 1 million deletions add up in Rust. 
- Total time spent in just creating 1M of 1k node linked list (without gaps/delays)
	- This is the total time it spent on just the creation of 1k node linked lists. Here, Java is 2.4x faster than Rust. This indicates that even pure allocation (without deallocation) is costlier in Rust than in Java. The reason is that Java's generational GC uses [**bump-pointer allocation**](https://shipilev.net/jvm/anatomy-quarks/4-tlab-allocation/) for short-lived objects — allocating a new object is nearly free, just incrementing a pointer into the young generation heap. Rust, by contrast, performs a heap allocation through its allocator for every `Box::new`, which is typically slower than HotSpot's thread-local bump-pointer fast path for young objects. That per-node allocator overhead accumulates across 1000 nodes per list × 1 million iterations.
- Max time spent in creating one single 1k node linked list (including gap)
	- This is the most interesting metric. Here, Rust is almost 6280x better than Java. 
	- This is the **STOP THE WORLD PAUSE OF JAVA GARBAGE COLLECTOR**. Before allocating the node, Java needed to reclaim some space. Hence, [it stopped the application and asked GC to reclaim some space](https://shipilev.net/jvm/anatomy-quarks/3-gc-design-and-pauses/). So, for one of the creation steps, it took significantly longer. 
- Worst Gap between the individual iteration
	- Here also, Rust is almost 3900x better than Java. This is a continuation of the previous metric. Because GC worked for one of the creation attempts, that iteration time ballooned for Java. 
		- For Rust, every iteration is the same = allocation + *any work after allocation* + delete.
		- For Java, there is a magic step = (*Garbage Collection*) + allocation + *any work after allocation*
- Initial 50M node linked list creation time
	- It seems Rust is almost 1.5x faster in creating a huge single-shot list. I am not sure why that behavior is seen. One important timing note: `_linked_list` goes out of scope at the very end of `main`, after `start.elapsed()` is already captured. So the program's reported elapsed time does **not** include the cost of dropping the 50M node list — that drop happens outside the measured window.


## Validating with GC Logs

We can enable GC logs to understand how GC is behaving in Java. Here are the GC logs — let's try to understand whether the numbers match.

```
➜  simple-programs time java -Xlog:gc StopTheWorld
[0.003s][info][gc] Using G1
[0.040s][info][gc] GC(0) Pause Young (Normal) (G1 Evacuation Pause) 5M->5M(16M) 10.465ms
[0.056s][info][gc] GC(1) Pause Young (Normal) (G1 Evacuation Pause) 9M->9M(20M) 14.943ms
[0.075s][info][gc] GC(2) Pause Young (Normal) (G1 Evacuation Pause) 13M->12M(72M) 17.457ms
[0.130s][info][gc] GC(3) Pause Young (Normal) (G1 Evacuation Pause) 28M->28M(72M) 42.890ms
[0.157s][info][gc] GC(4) Pause Young (Normal) (G1 Evacuation Pause) 40M->43M(72M) 25.836ms
[0.178s][info][gc] GC(5) Pause Young (Concurrent Start) (G1 Evacuation Pause) 51M->51M(72M) 19.032ms
[0.178s][info][gc] GC(6) Concurrent Mark Cycle
[0.203s][info][gc] GC(7) Pause Young (Normal) (G1 Evacuation Pause) 59M->60M(228M) 22.891ms
[0.330s][info][gc] GC(8) Pause Young (Normal) (G1 Evacuation Pause) 108M->109M(228M) 97.542ms
[0.415s][info][gc] GC(9) Pause Young (Normal) (G1 Evacuation Pause) 145M->147M(228M) 80.128ms
[0.465s][info][gc] GC(10) Pause Young (Normal) (G1 Evacuation Pause) 167M->169M(228M) 46.356ms
[0.499s][info][gc] GC(11) Pause Young (Normal) (G1 Evacuation Pause) 185M->187M(684M) 31.950ms
[0.526s][info][gc] GC(6) Pause Remark 233M->233M(684M) 0.997ms
[0.574s][info][gc] GC(6) Pause Cleanup 315M->315M(684M) 0.039ms
[0.576s][info][gc] GC(6) Concurrent Mark Cycle 398.156ms
[0.917s][info][gc] GC(12) Pause Young (Prepare Mixed) (G1 Evacuation Pause) 339M->343M(684M) 330.662ms
[1.155s][info][gc] GC(13) Pause Young (Mixed) (G1 Evacuation Pause) 447M->451M(684M) 226.702ms
[1.321s][info][gc] GC(14) Pause Young (Concurrent Start) (G1 Evacuation Pause) 519M->521M(684M) 158.399ms
[1.321s][info][gc] GC(15) Concurrent Mark Cycle
[1.433s][info][gc] GC(16) Pause Young (Normal) (G1 Evacuation Pause) 569M->573M(2052M) 106.487ms
[2.493s][info][gc] GC(17) Pause Young (Normal) (G1 Evacuation Pause) 977M->979M(2052M) 845.976ms
[2.963s][info][gc] GC(18) Pause Young (Normal) (G1 Evacuation Pause) 1311M->1183M(2052M) 418.603ms
[3.101s][info][gc] GC(19) Pause Young (Normal) (G1 Evacuation Pause) 1459M->1194M(2052M) 96.162ms
[3.152s][info][gc] GC(20) Pause Young (Normal) (G1 Evacuation Pause) 1490M->1193M(4428M) 5.607ms
[3.431s][info][gc] GC(21) Pause Young (Normal) (G1 Evacuation Pause) 1713M->1193M(4428M) 1.118ms
[3.476s][info][gc] GC(15) Pause Remark 1523M->1523M(4428M) 0.737ms
[3.526s][info][gc] GC(22) Pause Young (Normal) (G1 Evacuation Pause) 1745M->1193M(4428M) 0.848ms
[3.685s][info][gc] GC(15) Pause Cleanup 1883M->1883M(4428M) 0.070ms
[3.696s][info][gc] GC(15) Concurrent Mark Cycle 2375.184ms
[4.578s][info][gc] GC(23) Pause Young (Prepare Mixed) (G1 Evacuation Pause) 3785M->1193M(4428M) 1.470ms
[4.909s][info][gc] GC(24) Pause Young (Mixed) (G1 Evacuation Pause) 3845M->1189M(4428M) 6.353ms
[5.236s][info][gc] GC(25) Pause Young (Normal) (G1 Evacuation Pause) 3841M->1189M(4428M) 1.434ms
[5.558s][info][gc] GC(26) Pause Young (Normal) (G1 Evacuation Pause) 3841M->1189M(4428M) 1.472ms
[5.882s][info][gc] GC(27) Pause Young (Normal) (G1 Evacuation Pause) 3841M->1189M(4428M) 1.258ms
[6.214s][info][gc] GC(28) Pause Young (Normal) (G1 Evacuation Pause) 3841M->1189M(4428M) 1.623ms
[6.540s][info][gc] GC(29) Pause Young (Normal) (G1 Evacuation Pause) 3841M->1189M(4428M) 1.357ms
[6.879s][info][gc] GC(30) Pause Young (Normal) (G1 Evacuation Pause) 3841M->1189M(4332M) 1.320ms
Elapsed: 6863 ms
Initial 50M list create time: 2497475 µs
Total For Loop time (1M x 1K): 4364742 µs
Total Delays between iteration: 3733728 µs
Worst Gap is: 420189 µs
Total Create time: 3678367 µs
Worst Create time: 420117 µs
java -Xlog:gc StopTheWorld  11.25s user 1.61s system 180% cpu 7.124 total
```

Yes, from the logs we can see that GC pauses are happening. We can map the worst gap we saw (~420ms) to GC(18) which took 418ms. Using the default heap means the JVM starts with 16M and slowly expands, leading to more pauses early on. We can use a fixed heap with `-Xms4G -Xmx4G` which reduces pause frequency by avoiding dynamic heap expansion. The biggest memory reclaim happens around GC(23) and GC(24), after which the GC stabilizes with quick cycles. By the time GC(23) and GC(24) happen, the long-lived 50M node list has likely already been promoted to the old generation. Those later mixed collections are reclaiming old-generation regions after concurrent marking. The quick cycles after that occur because most of the remaining work is collecting the short-lived 1k node lists.

| GC event | Pause | Phase |
|---|---|---|
| GC(0)–GC(17) | 10ms–845ms | During 50M list creation (captured in `init_time`) |
| GC(18) | 418ms | First loop pause — the worst gap |
| GC(19)–GC(20) | 5–96ms | Transitioning — heap expanding, pauses shrinking |
| GC(21)–GC(30) | 1–6ms | Stabilized — short-lived 1k lists collected cheaply |

## Conclusion

So, Java's throughput is good, but Rust is very deterministic. Here is what two LLMs had to say about these results:

```

- Claude:
  
This is a classic **throughput vs. latency tradeoff**:
- Java's GC optimizes for throughput (amortizes collection cost across many allocations)
- Rust's ownership model gives deterministic, near-zero pause times at the cost of slower aggregate destruction of long-lived heap structures

For real-time systems, games, trading, or audio — Rust's 145 µs worst case matters enormously. For batch jobs or web services that care about average throughput, Java wins here.
```

```
- Codex

Bottom line: this output says Java has much better allocation throughput for short-lived objects, while Rust gives much tighter pause-time behavior. It does not prove “Java is faster than Rust” generally; it proves HotSpot’s generational allocator is very good for this exact garbage-heavy workload.
```


Yes, this is a small program and extrapolating these results broadly would be unwise. But it does give some good insights. If we are looking for very deterministic latency in our applications or services, then Rust is a good fit. In this allocation-heavy workload, Java showed better overall throughput. So, we need not feel guilty about using Java as long as occasional latency spikes are within acceptable bounds.


---
- I have used LLM agents to review the draft. I have also taken help with rewording and rephrasing the sentences. I have also used it for doing research.