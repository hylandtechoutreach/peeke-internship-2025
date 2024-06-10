<div id="content">
  <p>This page is password protected. Enter the password below:</p>
  <input id="password" placeholder="password"><button onclick="enterPassword()">Enter</button>
</div>

<script>
pwInput = document.querySelector("#password");
contentContainer = document.querySelector("#content");

function revealPage() {
  contentContainer.innerHTML = 
`
<h1>DevTools</h1>
<p><a href="https://developer.chrome.com/docs/devtools">Chrome DevTools</a> is a set of web developer tools built directly into the Google Chrome browser. DevTools lets you edit pages on-the-fly and diagnose problems quickly, which helps you build better websites, faster. If you're using Chrome, you <i>probably</i> needed to use DevTools to reveal this page. Chrome isn't the only browser, though - almost every browser has some form of developer tools.</p>
<h2>Introduction</h2>
<p>Check out this <a href="https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools">quick guide</a> to learn some of the basics.</p>
<p>Since Chrome is recommended for this project, take a look at <a href="https://developer.chrome.com/docs/devtools/overview">what you can do</a> with Chrome DevTools.</p>
<h2>More</h2>
<p>There is a lot you can do with DevTools. Some of the specific features are highlighted here:</p>
<ul>
  <li>
    <a href="https://developer.chrome.com/docs/devtools/javascript">Debugging JavaScript</a>
  </li>
  <li>
    <a href="https://developer.chrome.com/docs/devtools/storage/localstorage">Working with localStorage</a>
  </li>
  <li>
    <a href="https://developer.chrome.com/docs/devtools/network">Inspecting network activity</a>
  </li>
</ul>
`;
}

function enterPassword() {
  if (pwInput.value === "ilove2hack") {
    alert("You're in 😎");
    revealPage();
  } else {
    alert("Wrong password. This website will self destruct in 5...");
    alert("4...");
    alert("3...");
    alert("2...");
    alert("1...");
    document.location.href = "https://cdn.mos.cms.futurecdn.net/V68V76a9bFGTy5HYoag4s9-320-80.gif";
  }
}

pwInput.addEventListener("keydown", e => {
  if (e.key === "Enter") {
    enterPassword();
  }
});
</script>
