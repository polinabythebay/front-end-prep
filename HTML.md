#### HTML Questions:

* What does a `doctype` do?
* What's the difference between standards mode and quirks mode?
* What's the difference between HTML and XHTML?
* Are there any problems with serving pages as `application/xhtml+xml`?
* How do you serve a page with content in multiple languages?
* What kind of things must you be wary of when design or developing for multilingual sites?
* What are `data-` attributes good for?
* Consider HTML5 as an open web platform. What are the building blocks of HTML5?

---

#### Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.

- localStorage and sessionStorage are both so-called WebStorages and features of HTML5.
- localStorage stores information as long as the user does not delete them.
- sessionStorage stores information as long as the session goes. Usually until the user closes the tab/browser.
- cookies are simply cookies, which are supported by older browsers and usually are a fallback for frameworks that use the above mentioned WebStorages.
- In contrast cookies can store way less information then WebStorages and the information in WebStorages is never transferred to the server.

--
* Describe the difference between `<script>`, `<script async>` and `<script defer>`.
* Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?
* What is progressive rendering?
* Have you used different HTML templating languages before?
