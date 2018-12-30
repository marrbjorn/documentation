###### CONTENTS
* ##### [Description for 'background' of this project](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#small-background);
* ##### [Requirements and setup notes](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#setup);
* ##### [Description for design of project-application](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#design-of-application);
* ##### [Example-steps to play with this project-application](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#how-to-work);
* ##### [Meanings and conclusion notes](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#meanings);
* ##### [Compared to OWASP Top Ten 2017](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#compare-to-owasp-top-ten);

Small background:
-----------------

This is more like a "template" (or PoC) rather than an "application".

    Design is still based on my too much small experience with all of this "development" things;

In addition, I am not really friendly with development.

Thus, I decided to make a no-frills application and do it with the help of some kind of "tricks" (just as a template-PoC);

-------

* Project available on the github page: https://github.com/marrbjorn/CyberSecurityCourse-2018

* and <a href="https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project">this page</a> will be as documentation of project;

* also shortcut for <a href="#owasp">Compare to OWASP Top TEN</a>;


Setup:
======
Get started can be with next steps:
-----------------------------------

**FIRST**: we should be able to work with https://cybersecuritybase.mooc.fi (which means properly configured IDE and other requirements);

<br />**SECOND**: download this project ( https://github.com/marrbjorn/CyberSecurityCourse-2018 ) as zip-file or by git-commands as usually.

<br />**THIRD**: unpack it (if you downloaded the zip-file) and open the project in the IDE (for example, with Netbeans: "File -> Open Project..." under the menu).
   
    Then do the "Clean and Build Project" (how it is called under the Netbeans);
    this will trigger downloading/creating target-files and properly build project;

<br />**FOURTH**: "Run" application when you need to work or required to do some steps with application.

    first launch may ask about main class - choose this default one.
    
- - - -
DESIGN OF APPLICATION
=====================

This is some kind of landing page for music-party/meeting (but mainly it is friendly service for music bands);

Each music band/musician is already registered to be part of this party (by design);

Service <ins>**does not**</ins> provides ability to add more bands (this can be covered by the other steps);

Service <ins>**does**</ins> provides its own access for each music-band/musician to be able to "invite listeners";

For example, it could be a "friend" or someone else (some kind of special listeners); 

As a result there will be list (database with "name" and "phone-number") of listeners invited by music-bands;

Service provides ability to see full list of these listeners*.

    *but this should be available just for administrators (of party/service/website);
    
- - - -

And practically no any other features or design at work.
So, there are not so many steps for critical attacks or total impact.

      but such design does not remove the points that:
        ->>> "vulnerable" things and 
        ->>> "vulnerable" design of things
      will add vulnerabilities or troubles to application. 
       and this:
        ->>> can be "exploited" or 
        ->>> not (but with a potential ability to be used).

<strong>This project will be with improve design and additional features later.
But main meanings will be with same design.</strong>

Next there are some of steps to play with application-project (to get a view of potential troubles or exploitation);

"How To Work" description is not always too clear; sorry for that.

With Java-files (or html-templates) I also added comments about the places what can be fixed (or how can be fixed);

Mostly covered some of "troubles" in design; But some of them are based on "meanings";
- - - -
HOW TO WORK
===========
First steps as a start:
<pre>
When we run the application under the IDE - we can to open it under the browser;
By <strong>default</strong> configuration: available at http://127.0.0.1:8080 
</pre>
<hr />
We will see the default login-page. 

To access the service - we must be authorized;

This possible to do with music-bands' credentials or by admin-access; 
<pre>
At this step - if credentials are not known to us - we can do some steps to try to 'find' them:
 * Fuzz the login forms (like if not strong passwords/logins there);
 * Fuzz URL-address (like if there may be other pages than login-page or pages not covered by the login-page);
 * Find something else.
 
 with this kind of project-application - any of these steps will be valid or helpful.
 Or there may be additional potential steps (if "credentials" are known already).
</pre>
* Tools like [Burp](https://portswigger.net/burp) or [OWASP ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) are able to provide the ability to configure fuzz-attack for both of meanings.

* "Other" steps may be with direct attack or with knowledge about this service/administrators.

* Additional steps are covered by the situation - if "one of registered accounts" does something "malicious".

<hr />

We are able to start from trying to find another available pages than login-form.

Because, time to time, there may be "forgotten debug-pages", "consoles", "backdoors" or other.

Usually it is based on misconfiguration or temporary mistakes;
<pre>
With proper result we were able to get "/hidden" page, which looks like development-debug page.
Something as temporary ToDo List at the time when website was maintaining before release;

This page was with "exclusion" for temporary-access (by antMatchers.permitAll).
As usage Java Spring security config feature http.authorizeRequests().
And, as result, "excluded" from login-form.

With this kind of project-application this is possible:
-> by mistake (like addition to css-access exclusion via not proper design);
-> or specially for "debug", but does not removed after the release;

So, page available at http://127.0.0.1:8080/hidden 
</pre>
<b><sub>This page with certain css-style and maybe with potential temporary freeze (sorry - if it will be like that);
It is based on some of CSS-tutorials from web. I tried with multiple platforms and mostly all is OK.</sub></b>

Hidden-page directly has meanings that should be available only to administrators (or service) teams.

And this page looks like a ToDo-list with entry-strings about some things. 

The page was not removed, not deleted or 'denied' for some reasons after temporary access-debug-time.

With this page we were able to get more interesting (or useful) information:

* There is a note "do not forget to remove page or do deny access";
  * <q><strong> ^ -> not completed. so, maybe other things too.</strong></q>
* There is a special URL for some of src-files where also ask for credentials;
  * <q><strong> ^ -> most likely there should be an access-rights check.</strong></q>
* There is a note "do not forget re-change debug admin:admin credentials";
  * <q><strong> ^ -> if the page is not "disabled" - so - maybe credentials too. </strong></q>
* There is a note "do not forget update CMS-framework";
  * <q><strong> ^ -> looks like that build of this CMS-framework was with a known vulnerability;</strong></q>
* And some other entry-strings;

<pre>
After the hidden-page was found.
And with additional potential points as:

  -> debug or default credentials (admin:admin);
   which may still be valid.
 
  -> URL to page with 'src-files' as ask for review from another team 
      ( http:/127.0.0.1:8080/formsrc?review=on );
   which is also covered by the login-form.
   and may be with some other protection-layers;
 
   -> information about CMS Framework 
      (and that vulnerable build of this CMS was in use);
    with this kind of project:
 we will go to think that there are
   known CMS and
   known vulnerability for this CMS;
 and design of vulnerability is
   publicly known "backdoor"-access credentials (as administrator-rights account);

Usually to see/find known vulnerabilities you can check:
  official websites, 
  cve-lists, 
  advisories and 
  other.
 
 So, maybe this CMS Framework build is also still not updated.
   "brief-search" for this vulnerability gives the result that backdoor-credentials are (CMS:CMSpassword).
</pre>

We have some information already and the ability to try to do something.

"src"-page is covered by login-form (and looks like there is STRING-check under the parameter query by GET-method);

Available some of steps: "registered"-account will try to open this URL; anyone else; admin-account or some of tricks.

So, we are able to check: what if CMS Framework is not updated and to try to use "backdoor"-credentials from outdated build.

Open the URL with "src"-files from "/hidden"-page and get login-form.

Type "CMS"-as-login and "CMSpassword"-as-password;

So, we'll get access denied.... most likely there is a check for something (but credentials are valid).

Go back to hidden page (and then to src-review page) or from login-form directly (good to 'clear' session).

and try to use "admin:admin" for this special-src page.

Page is loaded and we got view of some src-file. Looks like it is html-template for some page.

<pre>
This page should work as temporary storage for src-files to be reviewed by another team;

Most likely randomly the page has not been removed (or even mistakenly open).
Even there are some of the "layers" of protection-access
(but is not too much proper and is not valid for this situation);

As a result of knowledge about admin-debug-credentials (from forgotten debug-page):
we are able to review src of html-template file.
</pre>
<hr />

We can directly study this html-template src-file or try to log in and check what can be done on the service.

Do not close the page with src-file and open a fresh tab with the login-form.

And use any of the credentials already known to us (admin:admin or CMS:CMSpassword).

Possible to suspect that there may be other not strong passwords (music band's account).

With current try - we are able to think that music bands with "strong" passwords.

<pre>with login-page http://127.0.0.1:8080  and valid credentials</pre>

We are able to get form-page; something like welcome-page.

      http://127.0.0.1:8080/form

Where possible to read information-words and to invite a listener (as music band's friend or other);

Go check "enter" from first! Ok, we got information that name-field is required.

Fill it and we were able do not fill "phone"-field.

But go try to fill it (or both of them) with tricks like "html-tags or scripts"

So, with this step <code>name</code> can be (as "alert" script): 

     <script>alert('name')</script>

And <code>phone</code> can be (as "alert" script):

     <script>alert(document.cookie)</script>
     
Fill it and transfer to application.

We get result-page of this action, where information-words and menu with three URLs:

* Add some else listeners;
* Re-login;
* And strange named URL (?!);

<hr />

<pre>
In this step we can return to known page with src-file.
And review it.

Possible to see potential trouble with handling output data from database about phones.

There visible that for somewhat reasons output text for phones comes as "unescaped text".
Based on the usage Thymeleaf (Java/HTML template engine) features.

In certain situations this can be useful - but not sure - that it can be helpful there.

Looks like that:
</pre>
        
       <td th:utext="${listener.phone}"><code>Listener phone</code></td>
    
<code>th:utext</code> probably comes there randomly (or for temporary debug);

This situation will create a potential ability to do <strong>Cross-Site Scripting (XSS)</strong>

Name field with proper output handling as <code>th:text</code> (escaped text).

Thus, with previous fill-action will be the situation that when someone is able to see list of listeners:

he will get an alert from "phone"-field (and "string" under the "name"-column).

This troublepoint possible to use for any other actions and reasons (with larger impact).

Looks like that it is a page with full table of listeners.

And just because it was asked for review - maybe under the debugging.

-------

So, back to the dreams about "strange named URL" under the "thanks-menu" after transferring listener.

URL's menu-description with strange words: <q><strong>Do you remember fylkr's song "do The Trick" from album "trick"?</strong></q>

and URL (page which can not be displayed) to 

<pre>http://127.0.0.1:8080/fylkr</pre>

We are also able to find that under the "form-thanks" html-page (as src of page) for this URL/menu-tab there are the next strings:
           
      <div sec:authorize = "hasAuthority ('ADMIN')">

Which should means that current point should only be visible to admins... but there is a mistake with the design.

And this 'entry' is visible for all.

Possible to suspect that it is else one temporary-debug (or under construction) page.

And knowing that there is mistake and page might be there (and most likely strange words are tips):

we are able to start thinking around.

There were already some pages with "string"-checks under the GET-methods.

And it looks like there might be something around it.
We can re-login with admin credentials.

But because there is already a mistake with checks - so - maybe the page will be available to anyone.

<pre>
We have a potential debug-URL with debug-tips.

Words says about fylkr's (and URL with /fylkr page-name) song "do The Trick" from album "trick".
Go to think that there are tips about how to do build a GET-query or how URL should looks like for proper result.

After some tries we were able to get proper configuration for this:

http://127.0.0.1:8080/fylkr?trick=doTheTrick 
</pre>

When we open this URL after previous actions - firstly - we get an alert. With xsrf-token-cookie.

And after that we will get a full table with all invited listeners.
 <sub>(Donald Duck included, where "Donald" is name  and "Duck" is phone)</sub>

In fact - page should be visible just for administrators.

Looks like that there is just one protection-layer: GET / "parameter"-string from user's browser.

For this type of "hidden" pages should be more secure protection in fact.

Then possible to play around CSRF and to perform redirect.

Someone is reported about potential vulnerable points and it is placed with next URL:

    http://127.0.0.1:8080/csrfiner
    
Where textarea is about PoC (html-template). Possible to get this content and to create .html-file;

Then possible to use it with both meanings: against GET-method and against POST-method;

With first form: we are able to add URL and redirect is happened.

With second form: required to capture XSRF-token-cookie (possible with cross-site-scripting);

With our internal tries - possible to get xsrf-token-cookie from browser's console. Then fill "name", "phone" and xsrf-token.

With "Go!"-button -> fresh listener is added. 'broken' csrf protection.

There enabled CSRF-protection, but with specific option as:

    csrfTokenRepository(CookieCsrfTokenRepository);

As result will be something like "CSRFtoken as cookie";

As feature - this is can be helpful and good.

But it is also with additional "option"; so result will be as:

    http.csrf().csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse()); 

This will trigger situation that if application will be with Cross-site-scripting troublepoint: then possible to get CSRF-token (based on disabled HttpOnly for this Csrftoken-cookie); 

And open redirect is part of mapping-feature with 'trouble'-design.
<hr />

MEANINGS
========

This project is an application with some troubles, vulnerable points and misuse of the design of things.

All these points (and tricks) make it possible to exploit it.

Mainly with this kind of "template/PoC" there is missing too much critical exploitation or attack-points.

But can be seen as "potential" troubles or things that need to be fixed anyway.

Because it can be critical later...

There is next list of main troublepoints and additional troubles (which can be less likely with exploitation or not so visible):

<ul>
<li><code>debug-todo-page is not deleted or is not properly denied</code></li>
<br />
<li><code>page-for-administrators-only is protected only by the GET-parameter string</code></li>
<br />
<li><code>unescaped output-text for phone-field</code></li>
<br />
<li><code>csrf-protection (provided by Spring framework) with 'broken' design</code></li>
<br />
<li><code>so called "Powerful Custom CMS v2" with known vulnerability</code></li>
<br />
<li><code>Mapping feature with 'unvalidated redirect'-trouble based on trouble-design</code></li>
<br />
<li><code>passwords are not encrypted 'at all'</code></li>
<br />
<li><code>HTTPS is missing</code></li>
<br />
<li><code>"http.cors()" with disabled status and "http.headers()" with custom partly trouble-design</code></li>
<br />
<li><code>h2-console is available for opening using this our 'internal' tries. during only our local tries</code></li>
<br />
<li><code>some of proper features have not been added</code></li>
<br />
<li><code>there may be some crash-situations</code></li>
</ul>

About first two points:
---
<pre>
it is already a troublepoint... 
but also, as result, there start be visible a lot of other troublepoints.
something like critical information has become randomly visible.

also list of all listeners (which should be just for administrators)
is visible for all who know proper string.
it is potential mistakes or not proper usage design 
(or just do not using proper design)...

debug-page (with critical data) is available for all.

and page just for administrators:
is not protected by something more than GET-query-string from user's browser.
</pre>

About unescaped/escaped text output and CSRF:
---
<pre>
phone-field with unescaped output text:
adds ability for exploiting situation by Cross-Site Scripting (XSS).

if application will be with other related troublepoints: will be more higher risk-usage.
A lot of steps to prevent it (for example, by frameworks in use - Spring or Thymeleaf);

CSRF protection is enabled with project (by Spring framework);
 
With this design - covered mainly only POST/DELETE request forms. And ignored GET-request forms.

If we would like to use csrf-token for GET-request forms - possible to add it with HTML template;

Thymeleaf will provide this feature. And I 'tried' to use it as input-hidden form.
 
Generally, this is worst design - because GET-method for critical things.... not nice.
 
Then CSRF protection with certain setting about cookie/csrf-token (with HttpOnly-disabled).
 
As result - possible to get this kind of "cookie" by scripts.
 
So, CSRF protection for POST-request forms is works. And kind of try to use csrf-tokens for GET-requests.
 
But we are, anyway, able to do CSRF-attack for this GET-request form.

And we are, anyway, able to do CSRF-attack for POST-request form - if "csrf-tokens" will be known for us.

With Cross-Site-Scripting trouble under the project-application - quite likely to perform it.
 
Thus, we are able to exploit and did the CSRF attack with this project-application based on points:
 
>> GET-request forms do not really protected by CSRF-tokens;

>> POST-request forms vulnerable if possible to get csrf-cookie-token (by using Cross-site-scripting as example).
 
Some of these points can be more critical when we decided to add log-out 
(on current time there is vulnerable "mapping" and "add listener" functionality only);
 
Also with enabled CSRF protection and with default state about database-console:
hibernate/h2-console access will be 'broken' based on points that CSRF-tokens is missing with login there;
</pre>

About vulnerable "potential" CMS:
---
<pre>This is just "meanings". Just like if this project-application using CMS (v2).
　
And this CMS with known vulnerability (backdoor-admin-rights credentials).
　
And application is not updated... though current build of "this CMS" is "v5".
　
So, too much outdated in fact. :) 

Another more real point is 'outdated' template (provided by course).

Possible to launch dependency-check ( https://www.owasp.org/index.php/OWASP_Dependency_Check )
how it was explained with course series.

as result - possible to see that some of dependencies with known vulnerabilities.
for example, outdated builds/dependencies:
logback-core-1.1.7.jar ; tomat-embed-core-8.5.6.jar ; groovy-2.4.7.jar ; spring-boot-1.4.2
and some more components; some of them are about one CVE.

but, of course, it is not always applied to all applications with this outdated dependencies.

possible that vulnerabilities are unrelated with application's design.
</pre>

About the other points:
---
<pre>
Passwords are not encrypted (or if it is - not salted). Not protected properly.
If there will be access to database (or hack it):
it will be just passwords with normal view.

HTTPS is missing - so:
can be visible all things between browser and application with less steps to do the trick.

default console-access for built-in SQL/hibernate database is enabled:
and available to be opened with this 'internal' tries.

there are many features that have not been added yet:
For example, "logout" and many other required things (logging, protection against automated attacks).

design of some steps will create a potential crash-situation. 
Time to time this may be too much critical.

http.headers() is implemented with partly broken design. also http.cors() with disabled state.
http.headers().defaultsDisabled().contentTypeOptions() only used;
Potential content sniffing is valid! 
Since there is "form.html" where we used 'title' before meta-charset-tag.

Mapping with current view: just kind of "trick"-feature;
But provides additional steps to "play" with project-application;
And weakness like unvalidated / open redirects.
</pre>
<hr />
<hr />

<h1 id="owasp"><ins>Compared to OWASP Top TEN</ins></h1>

This project application may be vulnerable to some kind of attacks.
Or may be with vulnerabilities, troublepoints or mistakes.

Compared to OWASP and their Top Ten 2017 ( https://www.owasp.org/index.php/Top_10_2017-Top_10 ) here may be the next ones:

<b>Broken Authentication</b> <strong>||</strong> <b>Sensitive Data Exposure</b>
<br /><sub>"Application functions related to authentication and session management are often implemented incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users' identities temporarily or permanently."</sub><br />
<sub>"Many web applications and APIs do not properly protect sensitive data. Attackers may steal or modify such weakly protected data. Sensitive data may be compromised without extra protection, such as encryption at rest or in transit, and requires special precautions when exchanged with the browser."</sub>
<br /><pre>as OWASP A2 and OWASP A3</pre>

There is totally not a proper work with passwords (encryption or hashing is missing; and not encrypted passwords are stored);

Missing encryption between application and browser (visible under the browser-console and as HTTP-protocol).

It is will be more visible by using sniffers. Or with popular software for analysing web-traffic (like Wireshark);

Not handled logout and some other related things. As result stuck for "session"-access;

For fix these points - we are able (as example) to use features, which provided by [Spring Framework](https://spring.io/).

I added comments for project-application with places that can be removed or added.

Also, there is potential situation for "hack" password database.

Mainly there we are able to use good "encryption"-methods for passwords and store it as encrypted ones (properly).

More nice to use salt in addition to encryption.

Better to prevent most of common automated attacks, do not allow to use weak passwords.

Good to use secure connection (TLS) also. And to introduce well-enough two step verification or 2FA option.
<hr />

<b>Cross-Site Scripting (XSS)</b>
<br /><sub>"XSS flaws occur whenever an application includes untrusted data in a new web page without proper validation or escaping, or updates an existing web page with user-supplied data using a browser API that can create HTML or JavaScript. XSS allows attackers to execute scripts in the victim's browser which can hijack user sessions, deface web sites, or redirect the user to malicious sites."</sub>
<br /><pre>as OWASP A7</pre>

There is not really proper escaping for user input data. For one of forms (phone-field).

Which goes be under the table of all listeners.

For prevent it with current project-application:

we were able to use "Thymeleaf" (Java/HTML template engine) with proper configuration about.

I also added comments about "potential" fix under the project-application.

Mainly it should be enough to re-change "th:utext" to "th:text" under the fylkr.html-template.

So, potential Cross-Site Scripting attack will require more actions, steps and advanced trick. 
<hr />

<b>Security Misconfiguration</b>
<br /><sub>"Security misconfiguration is the most commonly seen trouble. This is commonly a result of insecure default configurations, incomplete or ad hoc configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information. Not only must all operating systems, frameworks, libraries, and applications be securely configured, but they must be patched/upgraded in a timely fashion."</sub>
<br /><pre>as OWASP A6</pre>

This is the main troublepoint for current project-application.

Start from this - we are able to get some more things.

But it is already with some of critical (as common sense) things like:

- default-debug admin credentials (admin:admin); 

- unused debug pages with critical information ("/hidden");

- disabled good security features like http.cors() and certain http.header(). options;

- unpatched tools in use ("potential" CMS);

- default SQL/hibernate console is opened (internally);

- is not properly handling crash-situation;

- some designs are not properly used and other;
<hr />

<b>Broken Access Control</b> <strong>||</strong> <b>Insufficient Logging and Monitoring</b>
<br /><sub>"Restrictions on what authenticated users are allowed to do are often not properly enforced. Attackers can exploit these flaws to access unauthorized functionality and/or data, such as access other users' accounts, view sensitive files, modify other users' data, change access rights, etc."</sub><br />
<sub>"Insufficient logging and monitoring, coupled with missing or ineffective integration with incident response, allows attackers to further attack systems, maintain persistence, pivot to more systems, and tamper, extract, or destroy data."</sub>
<br /><pre>as OWASP A5 and OWASP A10</pre>

Possible to get and see information about "content, which not planned to be visible to certain user";

And for this - possible to use only "user's browser" and action for GET content (what should be covered).

Not enough checks, protection-checks and also some mistakes with design of it.

Most of these places - I marked under the project-application.

To fix it - possible to do a lot of steps (different ones) and required to choose...

Usually based on "design" of application. And importance of certain layer.

Basically, good to use all recommended secure things (accordingly to documentation) from first.

In addition, possible to use tools like static analysis tool or even dynamic analysis tool.

Quality control and other testing meanings are pretty valuable too.

Logging, auditing and monitoring is critical for web-based applications.

Possible to use specific tools like WAF as already kind of protection layer.

Furthermore received logs, information and suspicious events are should be handled for further checks.

Current project application is not about anything like this at all.
<hr />

<b>Using Components with Known Vulnerabilities</b>
<br /><sub>"Components, such as libraries, frameworks, and other software modules, run with the same privileges as the application. If a vulnerable component is exploited, such an attack can facilitate serious data loss or server takeover. Applications and APIs using components with known vulnerabilities may undermine application defenses and enable various attacks and impacts."</sub>
<br /><pre>as OWASP A9</pre>

For this project-application we were able to think that there is "CMS" in use.

And build of this CMS with known vulnerability.

Where trouble is "publicly known" backdoor-admin-account credentials.

CMS is not updated and "account" is not disabled.

Additionally, course-template with outdated dependencies. Some of them with known vulnerabilities.

But it may be not applied to application's design directly (as vulnerability).
<hr />

This project application is also about OWASP TOP TEN 2013 troubles. 

<sub>CSRF and Unvalidated Redirects.</sub>

<b>Cross-Site Request Forgery (CSRF)</b>

CSRF-protection is not designed properly.

With current project-application - possible to perform some tricky POC-steps to exploit it.

Mainly based on potential ability to perform it against GET-method.

But, also, csrf-protection is re-implemented to custom view with xsrf-token-cookie.

Thus, possible to perform it against POST-method too (knowing xsrf-token-cookie of session).

For prevent it - we were able to use default security config feature by Spring Framework.

Or add additional checks/protection under the templates (Spring/Thymeleaf) or another steps.

I added notes for project application about these places (mostly).

As exploit-view: possible to check examples with CSRFiner.html file.

With unfixed "Cross-Site-Scripting" trouble - CSRF is pretty dangerous trick.
<hr />

<b>Unvalidated Redirects and Forwards</b>

The application with "Mapping"-feature. Where partly broken design.

It get URL (string) from GET-parameter and trying to perform redirect.

So, possible to do any redirects to any valid URL.

Good to perform filtering or allow only internal mapping. Do not use 'parameter' from GET-request.

For example, possible to use only pre-configured list of URLs for mapping.
<hr />
<hr />

<sub>
<strong>CyberSecurityCourse project-application for course series</strong>:
</sub>

<sub>
Cyber Security Base by University of Helsinki and MOOC.fi in collaboration with F-Secure Cyber Security Academy
</sub>
