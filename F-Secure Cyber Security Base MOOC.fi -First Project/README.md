###### CONTENTS
* ##### [Description for 'background' of this project](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#small-background);
* ##### [Requirements and setup notes](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#setup);
* ##### [Description for design of project-application](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#design-of-application);
* ##### [Example-steps to play with this project-application](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#how-to-work);
* ##### [Meanings and conclusion notes](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#meanings);
* ##### [Compared to OWASP Top Ten 2013](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project#compare-to-owasp-top-ten);

Small background:
-----------------

This is more like "template" (or PoC) than "application".

    Design is still based on my too much small experience with all of this "development"-things;

Also I am not really friendly with development.

So, I decided to do a no-frills application and with some kind of "tricks" (just like template-PoC);

-------

* Project available at the github page: https://github.com/marrbjorn/CyberSecurityCourse

* and <a href="https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project">this page</a> will be as documentation of project;

* also shortcut for <a href="#owasp">Compare to OWASP Top TEN</a>


Setup:
======
Get started can be with next steps:
-----------------------------------

**FIRST**: we need to be able to work with https://cybersecuritybase.github.io (which means proper configured IDE and other requirements);

<br />**SECOND**: download this project ( https://github.com/marrbjorn/CyberSecurityCourse ) as zip-file or by git-commands as usually.

<br />**THIRD**: unpack it (if you downloaded zip-file) and open the project in the IDE (for example, with Netbeans: "File -> Open Project..." under the menu).
   
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

Like "friend" or someone else (some kind of special listeners); 

As result there will be list (database with "name" and "phone-number") of listeners invited by music-bands;

Service provides ability to see full list of these listeners.

    but this should be available just for administrators (of party/service/website);
    
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
 
 with this kind of project-application - any of this steps will be valid or helpful.
 Or there may be additional potential steps (if "credentials" are known already).
</pre>
* Tools like [Burp](https://portswigger.net/burp) or [OWASP ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) are able to provide the ability to configure fuzz-attack for both of meanings.

* "Other" steps may be with direct attack or with knowledge about this service/administrators.

* Additional steps are covered by the situation - if "one of registered accounts" does something "malicious".

<hr />

We are able to start from trying to find another available pages than login-form.

Because, time to time, there may be "forgotten debug-pages", "consoles", "backdoors" or other.

Usually based on misconfiguration or temporary mistakes;
<pre>
With proper result we were able to get "/hidden" page, which looks like development-debug page.
Something as temporary ToDo List at the time when website was maintaining before release;

This page was with "exclusion" for temporary-access (by antMatchers.permitAll).
As usage Java Spring security config feature http.authorizeRequests().
And, as result, "excluded" from login-form.

With this kind of project-application it possible:
-> by mistake (like addition to css-access with not proper design);
-> or specially for "debug", but does not removed after the release;

So, page available at http://127.0.0.1:8080/hidden

</pre>
<b><sub>This page with certain css-style and maybe with potential temporary freeze (sorry - if it will be like that);
It is based on some of CSS-tutorials from web. I tried with multiple platforms and mostly all is OK.</sub></b>

Hidden-page directly has meanings that should be available only to administrators (or service) teams.

And this page looks like a ToDo-list with entry-strings about some things. 

The page was not removed, deleted or 'denied' for some reasons after temporary access-debug-time.

With this page we were able to get more interesting (or useful) information:

* There is a note "do not forget to remove page or do deny access";
  * <q><strong> ^ -> not completed. so, maybe other things too.</strong></q>
* There is a special URL for some of src-files which also ask for credentials;
  * <q><strong> ^ -> most likely there should be an access-rights check.</strong></q>
* There is a note "do not forget re-change debug admin:admin credentials";
  * <q><strong> ^ -> if the page is not "disabled" - so - maybe credentials too. </strong></q>
* There is a note "do not forget update CMS-framework";
  * <q><strong> ^ -> looks like that build of this CMS-framework was with a known vulnerability;</strong></q>
* And some other entry-strings;

<pre>
After the hidden-page was found.
And with additional potential points as:

  -> debug credentials (admin:admin);
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

So, we have some information and the ability to try to do something.

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

Most likely randomly the page has not been removed.
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

<pre>So, with login-page http://127.0.0.1:8080  and valid credentials</pre>

We are able to get form-page; something like welcome-page.

      http://127.0.0.1:8080/form

Where possible to read information-words and invite a listener (as music band's friend or other);

Go check "enter" from first! Ok, we got information that name-field is required.

So, fill it and we were able do not fill "phone"-field.

But go try to fill it (or both of them) with tricks like "html-tags or scripts"

So, with this step <code>name</code> can be (as "alert" script): 

     <script>alert('name')</script>

And <code>phone</code> can be (as "alert" script):

     <script>alert('phone')</script>
     
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

So, with previous fill-action will be the situation that when someone is able to see list of listeners:

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

So, this 'entry' is visible for all.

Possible to suspect that it is else one temporary-debug (or under-construction) page.

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

When we open this URL after previous actions - firstly - we get an alert.

And after that we will get a full table with all invited listeners.
 <sub>(Donald Duck included, where "Donald" is name  and "Duck" is phone)</sub>

In fact - page should be visible just for administrators.

Looks like that there is just one protection-layer: GET / "parameter"-string from user's browser.

For this type of "hidden" pages should be more protection in fact.

<hr />

MEANINGS
========

This project is an application with some troubles, vulnerable points and misuse of the design of things.

All these points (and tricks) make it possible to exploit it.

Mainly with this kind of "template/PoC" there is missing too much critical exploitation or attack-points.

But can be seen as "potential" troubles or things that need to be fixed anyway.

Because it can be critical later...

There is next main troublepoints and additional troubles (which can be less likely with exploitation or not so visible):

<ul>
<li><code>debug-todo-page is not deleted or is not properly denied</code></li>
<br />
<li><code>page-for-administrators-only is protected only by the GET-parameter string</code></li>
<br />
<li><code>unescaped output-text for phone-field</code></li>
<br />
<li><code>csrf-protection (provided by Spring framework) is disabled</code></li>
<br />
<li><code>so called "Powerful Custom CMS v2" with known vulnerability</code></li>
<br />
<li><code>passwords are not encrypted 'at all'</code></li>
<br />
<li><code>HTTPS is missing</code></li>
<br />
<li><code>h2-console is available for opening using this our 'internal' tries</code></li>
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

if application will be with other related troublepoints:
will be more higher risk-usage.
A lot of steps to prevent it (for example, by frameworks in use - Spring or Thymeleaf);

by default (with proper usage) Spring Framework with enabled CSRF-protection.
　
There is disabled-status for this feature under the security config.
　
But also does not "enabled" CSRF-protection (like tokens) under the html-templates.
　
So, there is disabled and not enabled "CSRF-protection"..
</pre>

About vulnerable "potential" CMS:
---
<pre>This is just "meanings". Just like if this project-application using CMS (v2).
　
And this CMS with known vulnerability (backdoor-admin-rights credentials).
　
And application is not updated... even current build of "this CMS" is "v5".
　
So, too much outdated in fact. :) 
</pre>

About the other points:
---
<pre>
Passwords are not encrypted. Not protected properly.
If there will be access to database (or hack it):
it will be just passwords with normal view.

HTTPS is missing - so:
can be visible all things between browser/application with less steps to do the trick.

default console-access for build-in SQL/hibernate database is enabled:
and available to be opened with this 'internal' tries.

there are many features that have not been added yet:
For example, "logout"-points and many other required things.

design of some steps will create a potential crash-situation. 
Time to time this may be too much critical.
</pre>
<hr />
<hr />

<h1 id="owasp"><ins>Compare to OWASP Top TEN</ins></h1>

This project application may be vulnerable to some kind of attacks.
Or may be with vulnerabilities, troublepoints or mistakes.

Compared to OWASP and their Top Ten 2013 ( https://www.owasp.org/index.php/Top_10_2013-Top_10 ) here may be the next ones:

<b>Broken Authentication and Session Management</b> <strong>||</strong> <b>Sensitive Data Exposure</b>

  <pre>as OWASP A2 and OWASP A6</pre>

There is totally not a proper work with passwords (encryption or hashing is missing; and not encrypted passwords are stored);

Missing encryption between application and browser (visible under the browser-console and as HTTP-protocol).

It is will be more visible by using sniffers. Or with popular software for analysing web-traffic (like Wireshark);

Not handled logout and some other related things. As result stuck for "session"-access;

For fix this points - we are able (as example) to use features, which provided by [Spring Framework](https://spring.io/).

I added comments for project-application with places that can be removed or added.

Mainly there we are able to use "encryption"-methods for passwords and store it as encrypted ones (properly).

Good to use secure connection (TLS) also. 

Also there is potential situation for "hack" password database.
<hr />

<b>Cross-Site Scripting (XSS)</b>

<pre>as OWASP A3</pre>

There is not really proper escaping for user input data. For one of forms (phone-field).

Which goes be under the table of all listeners.

For prevent it with current project-application:

we were able to use "Thymeleaf" (Java/HTML template engine) with proper configuration about.

I also added comments about "potential" fix under the project-application.

Mainly it should be enough to re-change "th:utext" to "th:text" under the fylkr.html-template.

So, potential Cross-Site Scripting attack will require more actions, steps and trick. 
<hr />

<b>Security Misconfiguration</b>

<pre>as OWASP A5</pre>

This is main troublepoint for current project-application.

Start from this - we are able to get some more things.

But it is already with some of critical (as common sense) things like:

- default-debug admin credentials (admin:admin); 

- unused debug pages with critical information ("/hidden"); 

- unpatched tools in use ("potential" CMS);

- default SQL/hibernate console is opened;

- is not properly handling crash-situation;

- some designs are not properly used and other;

<hr />

<b> Missing Function Level Access Control </b>

<pre> OWASP A7</pre>

Possible to get and see information about "content, which not planned to be visible";

And for this is possible to use only "user's browser" and action for GET content (which should be covered).

Not enough checks, protection-checks and also some mistakes with design it.

Most of this places - I noted under the project-application.

To fix it - possible to do a lot of steps (different ones) and required to choose...

Usually based on "design" of application.

<hr />
<b> Cross-Site Request Forgery (CSRF) </b>

<pre>as OWASP A8</pre>

There is not properly designed CSRF-protection.

With current project-application - possible to perform some tricky POC-steps to exploiting this.

Mainly based on "csrf.disabled" feature.

For prevent it - we were able to use default security config feature by Spring Framework.

Or add additional checks/protection under the templates (Spring/Thymeleaf) or another steps.

I added notes for project application about this places (mostly).

As exploit-view: we are able to do the "html"-template (or html-string) for "POST"-form to add "listener";

It is can be more critical with "Cross-Site-Scripting" trouble.

Possible to provide certain "description", but I will think to provide "extended" build of project.

Where CSRF-troublepoint will be with more interesting design (or some kind of this).

<hr />
<b> Using Components with Known Vulnerabilities</b>

<pre>as OWASP A9</pre>

For this project-application we were able to think that there is some of "CMS" in use.

And this "CMS build" with known vulnerability.

Where is "known" backdoor-admin-account credentials.

CMS is not updated and "account" is not disabled.
<hr />
<hr />

<sub>
<strong>CyberSecurityCourse project-application for course series</strong>:
</sub>

<sub>
mooc.fi Cyber Security Base by University of Helsinki in collaboration with F-Secure Cyber Security Academy
</sub>
