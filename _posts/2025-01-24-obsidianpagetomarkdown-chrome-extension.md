---
category: Technical
date: 2025-01-24
layout: post
title: Obsidian - Page to Markdown for bookmark
updated: 2025-01-24
---

I use Obsidian to bookmark the blog posts as well as any internet articles to read at a later point. When I add them to Obsidian, I use a particular format. Example -   

  

```  

[post title](post link)  
- Source: <website name>  
- Date: <current date added>  
- Notes: <>  
```  

Now to bookmark one or two pages is not a big deal to type all these details. But, as more pages need to be bookmarked, it becomes time consuming activity as well as it is an effort that has no value. So, I planned to automate this with a browser extension which can get me this blurb of markdown from an open webpage in the current tab. This was a nice to have project and I could not invest time on this for a while.  

Recently, I listened to the podcast of [AI tools for software engineers, but without the hype - with Simon Willison - The pragmatic Engineer Podcast](https://open.spotify.com/episode/0Zr65YYcw9ITADKlVDPsXS?si=fY_FCGZDTIK5VsT4TCcvLw). Inspired from this, I thought of experimenting with the Claude AI service. The browser extension project seemed a good fit to try it out.   

Given by one single line prompt - `Hi, I want to develop a small chrome extension which collect the title of page and actual link and present it in a particular markdown format` , it was able to generate the complete extension code with the exact steps of how to install and use it. I am very impressed by it. I have experience in using AI as coding assistant at work. At work, it generated bits and pieces of code - some functions or unit tests. But, this is the first time I am seeing it generate an entire application. I agree, it is a small application, but let's compare it to what if I did this without the AI. I need to spend time in investigating how to create a chrome extension. Then, I need to apply that knowledge in creating that extension. Definitely, 2-3 days of dedicated work. All of this got reduced to 2-3 minutes by AI now!!?

Once it generated this code, I did some small modifications to suit my needs. You can find the final code in the github repository - [ObsidianP2M](https://github.com/harsha-kadekar/ObsidianP2Mark).  Below are the details of the chrome extension - ObsidianP2M

## ObsidianP2M

This is a chrome extension to copy the current open tab website address in a markdown format which can be copied to the Obsidian.
This chrome extension is developed using Claude AI. The main purpose of this extension is for helping in bookmarking of the website pages in the Obsidian Vault.

We can use this extension on any open web page in the chrome based browser. Once used it will generate a markdown blurb in the format

```
[current tab title](current tab url)
- Source: current tab base address
- Date: current date in the format YYYY-MM-DD
```

Example, if you have opened a blog post in your browser's tab - [https://harsha-kadekar.github.io/book-summary-made-in-japan.html](https://harsha-kadekar.github.io/book-summary-made-in-japan.html), then on using ObsidianP2Mark extension, you can get markdown blurb as -

```
[Book Summary - Made In Japan - Akio Morita and Sony](https://harsha-kadekar.github.io/book-summary-made-in-japan.html)
- Source: harsha-kadekar.github.io
- Date: 2025-01-23
```

## How to Install
- Clone this github repository to your location
- In Chrome, go to chrome://extensions/
- Enable "Developer mode" in the top right
- Click "Load unpacked" and select the directory where this github repository was cloned extension

## How to Use
- Go to your favorite webpage or blog post in your browser
- Click on the extension ObsidianP2Mark in your browser. This should generate the markdown blurb.
- Click on the `Copy To Clipboard` button. This should copy the blurb to clipboard, which can be pasted in your Obsidian vault.

## How was this generated using AI?

The prompt I gave is `Hi, I want to develop a small chrome extension which collect the title of page and actual link and present it in a particular markdown format`.

The answer generated was -

```
I can help you create a Chrome extension that captures page information and formats it in Markdown. I'll create a simple extension that gets the current tab's title and URL.

// manifest.json
{
  "manifest_version": 3,
  "name": "Page to Markdown",
  "version": "1.0",
  "description": "Converts current page title and URL to markdown format",
  "permissions": ["activeTab"],
  "action": {
    "default_popup": "popup.html"
  }
}

// popup.html
<!DOCTYPE html>
<html>
<head>
  <title>Page to Markdown</title>
  <style>
    body {
      width: 300px;
      padding: 10px;
    }
    #markdownOutput {
      width: 100%;
      min-height: 50px;
      margin-top: 10px;
      resize: vertical;
    }
    button {
      margin-top: 10px;
      width: 100%;
      padding: 8px;
    }
  </style>
</head>
<body>
  <textarea id="markdownOutput" readonly></textarea>
  <button id="copyButton">Copy to Clipboard</button>
  <script src="popup.js"></script>
</body>
</html>

// popup.js
document.addEventListener('DOMContentLoaded', function() {
  // Get current tab info
  chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
    const currentTab = tabs[0];
    const markdownFormat = `[${currentTab.title}](${currentTab.url})`;

    // Display formatted markdown
    document.getElementById('markdownOutput').value = markdownFormat;
  });

  // Copy to clipboard functionality
  document.getElementById('copyButton').addEventListener('click', function() {
    const markdownText = document.getElementById('markdownOutput');
    markdownText.select();
    navigator.clipboard.writeText(markdownText.value);

    // Provide feedback
    const button = this;
    const originalText = button.textContent;
    button.textContent = 'Copied!';
    setTimeout(() => {
      button.textContent = originalText;
    }, 1500);
  });
});

To use this extension:

- Create a new directory for your extension
- Create these three files (manifest.json, popup.html, and popup.js) with the provided code
- In Chrome, go to chrome://extensions/
- Enable "Developer mode" in the top right
- Click "Load unpacked" and select your extension directory

When you click the extension icon, it will:

- Get the current page's title and URL
- Format them in Markdown style: [Title](URL)
- Display the formatted text in a textarea
- Provide a button to copy the formatted text to your clipboard
```