---
permalink: /books/
title: "Books"
toc: true
---

I read various kinds of books. It has taught me a lot and has been guiding me. One of the things I observed was, after reading the book I forget most of its content or main idea within few days. Also if the book was big and I took long time to finish it, by the time I reached the end of the book, I would have forgotten what I read in the beginning of the book. So it would be a good thought exercise for me to recap the book's content and write down the gist of it. So this page will hold the small gist or learnings I took away from reading that book.
{: style="text-align: justify;"}

All the books I read are bookmarked in [GoodReads](https://www.goodreads.com/harsha_kadekar)

### Release It! Design and Deploy Production-Ready Software
- Author: **Michael T. Nygard**
- GoodReads: [Release It!](https://www.goodreads.com/book/show/1069827.Release_It_)

As the name of the book implies, the main topic of this book is about how you will design your applications and services such that it can be deployed and maintained in a production environment. There are multiple factors which help for a good design 
* The stress, impulses or component failures will affect the integeration points of the application. And these integeration points will fail and this failure will spread to other parts of the application.
* Whenever you are connecting to remote applications or databases via sockets or RMI or any means we need to protect these connections with timeouts. These remote calls are unpredictable - it can fail with an error, it can take a lot of time to return or it can fail silently. So better to protect them with timeouts.
* Use circuit breakers to protect from the impulses, stress. Make sure there is way to know whether circuit breaker is activated - some kind of metric or alarm is needed.
* In web applications use sessions judiciously. Each session resides in the memory and it will reside for long time even if it is not used.
* If you are expecting high demand for certain resources or functionality then protect it such that those demands are diverted to a separate resource thus protecting the other functionality and components from getting affected due to resource crunch.
* Always use connection pool to connect to a resource whether it is multiple instances of services or database.
* Use ORM to connect and operate to the database. Never directly run a direct SQL query from your application.
* Before releasing to production do a load testing. And remember your development envrionment and QA environment will never be able to match scale of production. Rather than trying to match the scale of production, design your application code such that even in the hightened requests or stress, application should be able to transact.
* Slow responses from your application will lead to other problems like more traffic and customers will keep retrying and more resources are utilized leading to cascading failures. 
* Fail fast is better than slow responses.
* For slow responses, reason could be memory leaks or resource contentions like DB pool is filled up or thread pool is filled up.
* Do not blindly put an SLA to your services. Measure it. Understand the SLA of your dependent services. Based on that derive your SLA. You cannot give an SLA which is better than your dependent service.
* Use bulkheads in case of failures, so that even if some components fail your product is still running and insulated from the failed components.
* Caching has limits. It increases your services response to certain extent after that it will eat your memory and thus leading to decrease in response. So use it carefully.
* Make sure you clean up your old logs. Either move to a different location but do not allow it fill up space.
* Clean up your old data. Maintain data hygiene. 
* All these disk cleanup and application data clean up has to happen automatically via your application rather than human intervention.
* When you test, do not just go by your requirements. Go out of requirements when testing negative failure scenario. 
* Try to use intelligent load balancers that consistently does health checks of the underlying systems and based on bad health stops sending requests to those instances.
* Try to provide an adminstrative CLI tool for every service for ops work.
* Set up alarms and monitors like for system health, requests recieved, response time, max threads, max connections. There should be dashboard to monitor these metrics and alarms to give real time picture of what is happenning to your service or application. Logs are a great way to learn about what is happening but metrics & alarms give you high level picture of what is going on. Also have tools which will read your logs and alarms based on specific stack trace occurrence such as exceptions or faults being reported in logs.
* Releases should be done often and all the release activity should be automated - aim for continuous deployment.


### ಶಿಕಾರಿ Shikari
- Author: **Yashwant Chittal**
- GoodReads: [ಶಿಕಾರಿ Shikari](https://www.goodreads.com/book/show/25657010-shikari)

The book is about corporate politics. The main protagonist is hunted (ಶಿಕಾರಿ Shikari) from multiple directions. The narration of the story is also very different, as in everything is happening through the view point of the hero. It's as if I am part of the mind of the hero and listening to every thought that is getting generated in his mind. It gives clear picture of how the game of corporate politics and it's fight are fought, how each human relation is utilized for acheiving something in the corporate world, how a person becomes a pawn between the fights of heads. The thing which stood out is how it gives a clear picture of human greed and selfish nature. The moment when a person is in the path of losing, everyone will swoop in like vultures to take their revenge and also the moment humans come to know that you are a losing side, they will shift their allegiance. You and you alone are your friend. Its a good read.
{: style="text-align: justify;"}


### The Little Book Of Common Sense Investing
- Author: **John C Bogle**
- GoodReads: [The Little Book Of Common Sense Investing](https://www.goodreads.com/book/show/34003072-the-little-book-of-common-sense-investing)

Jobh C Bogle is founder and ex-chairman of Vangaurd. In this book he makes a very strong case for investing in low cost index funds. He gives lot of reasons why we should not try to trump the market returns. Following are the learnings I take from this book:
1. Do not do short term investing. Always aim for long term investing.
2. Investment should be diversified. A person will secure his returns if he owns all of the business available in the market.
3. Do not try to choose individual stocks and invest in it. It is a loosing game. Now index funds will provide the necessary diversification.
4. When you are investing, invest in low cost index funds which will provide the diversification and also has low cost, interms of tax and managing. Do not invest in high cost mutual/equity funds which would eat up all the returns in the cost of maintaining it. So only fund managers will earn money in it.
5. ETF are good option as long as it is targetted towards diversified portfolio like S&P 500 or US Total Stock market. These ETF should be again long term investments and not short term investments.
6. Remember your returns include the dividends which you get from investing in the fund. Those dividends should also be ideally reinvested. 
7. Initially when you start investing you should have ideally 80/20 Index Fund/Bond investment. As you progress towards your retirements, this share needs to be changed. Usually the ratio will reverse. 
8. From time to time you need to evaluate your investments and maintain that investment ratio. This investment can be still diversified like 40% in US Index Funds, 20% in Non US Market Funds and 20% in Bonds.
9. Remember do not invest emotionally. The market has a mean reversion - Every time market goes up it will come back down to its normal trajectory, similarly everytime market goes down it will come back up to its normal trajectory.


### Light on the Yoga Sūtras of Patañjali
- Author: **Patañjali (Commentator & Translator: B K S Iyengar)**
- GoodReads: [Light on the Yoga Sūtras of Patañjali](https://www.goodreads.com/book/show/139352.Light_on_the_Yoga_S_tras_of_Pata_jali)

B.K.S. Iyengar is famous for his Yoga practices. In this book, he has not only provided literal English translation of each of the sūtras, but also gives detailed explanation and commentary on it. The book gives systematic steps a person needs to take to achieve the Kaivalya ( individual self merges to universal self). There are different stages which the saadhaka needs to pass through by continuous saadhana. Every person based on his previous Saadhana and their nature, we can classify their level to 4 sections. In Yoga Sūtras, Patañjali has given four sections (Pāda) - Samadhi Pada, Saadhana Pada, Vibhuti Pada and Kaivalya Pada which can be adopted based on the maturity of practitioner. B.K.S. Iyengar explains the similarities between Bhagavad Geeta and Yoga Sutras. 
{: style="text-align: justify;"}

B.K.S. Iyengar gives one of the best explanation for the Abhyasa and Vairagya - "Abhyasa is a dedicated, unswerving, constant, and vigilant search into a chosen subject, pursued against all odds in the face of repeated failures for indefinitely long period of time. Vairagya is the cultivation of freedom from passion, abstention from worldly desires and appetites, and discrimination between real and the unreal. It is the act of giving up all sensuous delights. Abhyasa builds confidence and refinement in the process of culturing the consciousness, whereas vairagya is the elimination of whatever hinders progress and refinement. Proficiency in vairagya develops the ability to free oneself from the fruits of action." 
{: style="text-align: justify;"}

BKS also explains the importance of self discipline for a Saadhaka. Yoga is for reaching perfection in a human by means of using himself as the tool. "The disciplines of purifying man's three constituents, body, speech and mind constitute kriyayoga, the path to perfection. Our bodies are purified by self-discipline (tapas), our works by Self-study (svadhyaya) and our minds by love and surrender to Him (Isvara pranidhana)". One of the main misconception previaling is equating Yoga to asana. Asana is just small part of yoga,whereas Yoga is a whole system consisting of many things which needs to be practiced and cultivated to achieve the ultimate goal of Kaivalya. Yoga practioner gains following knowledge -  knowledge of the body, knowledge of energy, knoweldge of controlling the mind, stability in intelligence, knowledge gained by experience, absorption of the various flavours that life offers and knowledge of the self. By yogic practices the sadhaka conqures his body, controls his energy, restrains the movements of the mind and develops sound judgement, from which he acts rightly and becomes luminous. From this luminosity he develops total awareness of the very core of his being, achieves supreme knowledge, and surrenders his self to the Supreme Soul. 
{: style="text-align: justify;"}

As part of Yoga, we need to practice following things - Yama ( satya, ahimsa, non stealing, brahmacharya, freedom from avarice or non covetousness), Niyama (sauca - cleanliness, santosha - contentment, tapas - religious fervour, svadhyaya - study of scriptures & self, Isvara Parindhana - surrender of self to God), Asana, Pranayama and Pratyahara (Dharana, Dhyana and Samadhi). 
{: style="text-align: justify;"}

Dharana is concentration - pointed focus on something. Maintaining that concentration will lead to Dhyana. "When the object of contemplation shines forth without the intervention of one's own consciousness, dhyana flows into samadhi. When a musician loses himself and is completely engrossed in his music, or an inventor makes his discoveries when devoid of ego, or a painter transcends himself with colour, shade and brush; they glimpse samadhi. Similarly it is with the yogi: when his object of contemplation becomes himself, devoid of himself, he experiences samadhi." The difference is that the artist or musician reaches this state by effort and cannot sustain it; whereas the yogi, remaining devoid of ego, experiences it as natural, continuous and effortless. Consequently, it is difficult for an artist to infuse his vision of the sublime, which is associated with the performance and realization of a particular art form into his ordinary daily existence. For the yogi, however, whose 'art' is formless and whose goal has no physical expression like a painting, a book or a symphony, the fragrance of samadhi penetrates every aspect of his normal behaviour, activities and state of being.  Uninterrupted flow of attention dissolves the split between the object seen and the seer who sees it. Consciousness appears to have ceased, and to have reached a state of silence. It is devoid of 'I', and merges into the core of the being in a profound state of serenity. In samadhi, awareness of place vanishes and one ceases to experience space and time. When one contemplates a diamond, he at first sees with great clarity the gem itself. Gradually one becomes aware of the light glowing from its centre. As awareness of the light glows, awareness of the stone as an object diminishes. Then there is only brightness, no source, no object. When the light is everywhere that is samadhi.
{: style="text-align: justify;"}