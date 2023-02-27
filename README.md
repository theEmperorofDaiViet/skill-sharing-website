<a name="readme-top"></a>
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#key-features">Key Features</li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

<p align="center">
    <img src="public\images\logo.png" width="128">
</p>

# About The Project
The skill-sharing website from chapter 21 of the famous book about JS - "Eloquent JavaScript", with a few additional features.

<p align="center">
    <img src="public\images\cover.jpg" width="175">
</p>

## Built With
* [![HTML5][HTML5-shield]][HTML5-url]
* [![CSS3][CSS3-shield]][CSS3-url]
* [![JavaScript][JavaScript-shield]][JavaScript-url]
* [![Node.js][Node.js-shield]][Node.js-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

# Getting Started

## Prerequisites
Before cloning and using this application, you'll need to install these things on your computer:
* [Node.js](https://nodejs.org/en/download/): a single-threaded, open-source, cross-platform runtime environment for building fast and scalable server-side and networking applications. It runs on Chrome's V8 JavaScript runtime engine, and it uses event-driven, non-blocking I/O architecture, which makes it efficient and suitable for real-time applications.
* [node-static](https://www.npmjs.com/package/node-static): a simple, <i>rfc 2616 compliant</i> HTTP static-file server module for Node.js, with built-in caching. You can install this package by typing this command in terminal:
    ```sh
    npm install node-static
    ```
* [Visual Studio Code](https://code.visualstudio.com/download): You can choose any IDE or Text Editor that you want. To build a simple application like this, I recommend <b>Visual Studio Code</b>.

## Installation
You can install this application by cloning this repository into your current working directory:
```sh
git clone https://github.com/theEmperorofDaiViet/skill-sharing-website.git
```
After cloning the repository, you can open the project by Visual Studio Code.

Open a terminal and type this command:
```sh
node skillsharing_server.js
```
Then open a browser window for <i>http://localhost:8000/</i> to go to the skill-sharing website! I chose port 8000. You can switch to another port by changing the port number in [/skillsharing_server.js](skillsharing_server.js/#L162).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

# Key Features
## Goal
><i>A <b>skill-sharing</b> meeting is an event where people with a shared interest come together and give small, informal presentations about things they know. At a gardening skill-sharing meeting, someone might explain how to cultivate celery. Or in a programming skill-sharing group, you could drop by and tell people about Node.js. Such meetups are a great way to broaden your horizons, learn about new developments, or simply meet people with similar interests.</i>

<p>Our goal is to set up a website for managing talks given at a skill-sharing meeting. Imagine a small group of people meeting up regularly in the office of one of the members to talk about unicycling. The previous organizer of the meetings moved to another town, and nobody stepped forward to take over this task. We want a system that will let the participants propose and discuss talks among themselves, without a central organizer.</p>

## Design
<p>There is a <i>server</i> part, written for Node.js, and a <i>client</i> part, written for the browser. The server stores the system’s data and provides it to the client. It also serves the files that implement the client-side system.</p>

<p>The server keeps the list of talks proposed for the next meeting, and the client shows this list. Each talk has a presenter name, a title, a summary, and an array of comments associated with it. The client allows users to propose new talks (adding them to the list), delete talks, and comment on existing talks. Whenever the user makes such a change, the client makes an HTTP request to tell the server about it.</p>

<p>The application will be set up to show a <i>live</i> view of the current proposed talks and their comments. Whenever someone, somewhere, submits a new talk or adds a comment, all people who have the page open in their browsers should immediately see the change. This poses a bit of a challenge - there is no way for a web server to open a connection to a client, nor is there a good way to know which clients are currently looking at a given website. A common solution to this problem is called <b><i>long polling</i></b>, which happens to be one of the motivations for Node’s design.</p>

When a request matches none of the request types defined in our [router](router.js), the server must interpret it as a request for a file in the :open_file_folder:<b>public</b> directory. I used [node-static](https://www.npmjs.com/package/node-static) - a solid, well-tested static file server from NPM. This isn’t the only such server on NPM, but it works well and fits our purposes.

<p>The skill-sharing server in <code>v1.0.0</code> keeps its data purely in memory. This means that when it crashes or is restarted for any reason, all talks and comments are lost. In <code>v1.1.1</code>, the server was extended so that it stores the talk data to disk and automatically reloads the data when it is restarted.</p>

<p>The wholesale redrawing of talks works pretty well because you usually can’t tell the difference between a DOM node and its identical replacement. But there are exceptions. If you start typing something in the comment field for a talk in one browser window and then, in another, add a comment to that talk, the field in the first window will be redrawn, removing both its content and its focus. In a heated discussion, where multiple people are adding comments at the same time, this would be annoying. <code>v1.2.0</code> solved it.</p>

<p><code>v1.3.0</code> provided a little more friendly user interface.</p>

<p align="right">(<a href="#readme-top">back to top</a>)</p>

# Usage

<p align="right">(<a href="#readme-top">back to top</a>)</p>

# Contact

You can contact me via:
* [![GitHub][GitHub-shield]][GitHub-url]
* [![LinkedIn][LinkedIn-shield]][LinkedIn-url]
* ![Gmail][Gmail-shield]:&nbsp;<i>Khiet.To.05012001@gmail.com</i>
* [![Facebook][Facebook-shield]][Facebook-url]
* [![Twitter][Twitter-shield]][Twitter-url]

<br/>
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- Tech stack -->
[HTML5-shield]: https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white
[HTML5-url]: https://www.w3.org/html/
[CSS3-shield]: https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white
[CSS3-url]: https://www.w3.org/Style/CSS/
[JavaScript-shield]: https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E
[JavaScript-url]: https://www.ecma-international.org/
[Node.js-shield]: https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white
[Node.js-url]: https://nodejs.org

<!-- Contact -->
[GitHub-shield]: https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white
[GitHub-url]: https://github.com/theEmperorofDaiViet
[LinkedIn-shield]: https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white
[LinkedIn-url]: https://www.linkedin.com/in/khiet-to/
[Gmail-shield]: https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white
[Facebook-shield]: https://img.shields.io/badge/Facebook-%231877F2.svg?style=for-the-badge&logo=Facebook&logoColor=white
[Facebook-url]: https://www.facebook.com/Khiet.To.Official/
[Twitter-shield]: https://img.shields.io/badge/Twitter-%231DA1F2.svg?style=for-the-badge&logo=Twitter&logoColor=white
[Twitter-url]: https://twitter.com/KhietTo