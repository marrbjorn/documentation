Small background:
-----------------

This is more like "template" (or PoC), than "application" in fact.

    Design based on my too much small experience with all of this "development"-things;

Also I not really friendly with development.

So I decided to do not hard designed application and with some kind of "tricks" (as can be just like template-PoC);

-------

Project available at the github page: https://github.com/marrbjorn/CyberSecurityCourse

--> and <a href="https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project">this page</a> will be as documentation of project;

and shortcut for <a href="#owasp">Compare to OWASP Top TEN</a>


Setup:
======
Get started can be with next steps:
-----------------------------------

<b>FIRST</b>: we have to be able work with https://cybersecuritybase.github.io (which means proper configured IDE and other requirements);

<br />
<strong>SECOND</strong>: download this project ( https://github.com/marrbjorn/CyberSecurityCourse ) as zip-file or by git-commands as usually.

<br /><b>THIRD</b>: unpack it (if downloaded zip-file) and open project under the IDE (with Netbeans: "File -> Open Project..." under the menu).
   
    Then do the "Clean and Build Project" (how it called under the Netbeans);
    this will trigger downloading/creating target-files and properly build project;

<br />
<strong>FOURTH</strong>: "Run" application, when required work or required to do some steps with application.

    first launch may ask about main class - choose this default one.
    
<hr />
DESIGN OF APPLICATION
=====================
=====================

There is some kind of landing page for music-party/meeting (but mainly friendly service for music bands);

Each music band/musician already registered to be part of this party (by design);

Service <ins>do not</ins> provide ability to add more bands (this is can be covered by the other one steps);

Service <ins>do</ins> provide own access for each music-band/musician to be with ability "invite listeners";

Like "friend" or someone else (some kind of special listeners); 

As result there will be list (database with "name" and "phone-number") of listeners, which invited by music-bands;

Service provide ability to see full list of this listeners.

    but this is should be available just for administrators (of party/service/website);
    
<hr />

There is practically missing any other features or design at work.
And for critical attacks or total impact there is not so many steps.

      but this is do not remove points that:
        -> "vulnerable" things and 
        -> "vulnerable" design of things
      will add vulnerabilities or troubles to application. 
       and this is:
        -> can be "exploited" or 
        -> not (but with potential ability do that).

<strong>This project will be with improve design and additional features later.
But main meanings will be with same design.</strong>

There is some of steps to play with application-project (for get view of potential troubles or exploiting it);

Under the Java-files (or html-templates) I also added comments about places, which can be fixed (or how can be fixed);

This is mostly covered some of "troubles" in design; But some of them based on "meanings";
<hr />
HOW TO WORK
===========
First steps as start can be like that:
<pre>
When we run application under the IDE - we able to open it under the browser;
By <strong>default</strong> configuration: available at http://127.0.0.1:8080 
</pre>
<hr />
We will be with default login-page. 

For access to service - we have to be authorized;

This is available to do by music-bands' credentials or by admin-access; 
<pre>
At this step - if credentials do not known for us - we able to do some of steps for get access:
 -> Fuzz the login forms (if there is not strong passwords/logins);
 --> Fuzz URL-address (if there can be other pages, than login-page or which do not covered by login-page);
 ---> Found something else.
 
 with this kind of project-application - any of this steps will be valid or helpful.
 Or can be additional potential steps (if "credentials" known already).
</pre>
<ul>
<li>Tools like Burp or OWASP ZAP able to provide ability to configure fuzz-attack for both of meanings.</li>

<li>"Other" steps can be with direct attack or knowledge about this service/administrators.</li>

<li>Additional steps covered by situation - if there is "one of registered accounts" do something "malicious".</li>
</ul>

<hr />

We able to start from trying to find another available pages, than login-form.

This is can be "forgotten debug-pages", "consoles", "backdoors" or other.

Usually this is based on misconfiguration or temporary mistakes;
<pre>
With proper result we able to get "/hidden" page, which looks like development-debug page.
Mainly as temporary ToDo List at the time, when website was maintaining before release;

This page was as "exclusion" for temporary-access (by antMatchers.permitAll).
As usage Java Spring security config feature http.authorizeRequests().
And "excluded" from login-form.

With this kind of project-application it possible:
-> by mistake (as additional to css-access with not proper design);
-> or specially for "debug", but do not removed after the release;

So page available at http://127.0.0.1:8080/hidden

</pre>
<b><sub>Mainly this page have css-style-work, which maybe can to create temporary freeze (sorry - if it will be like that);
this is based on some of CSS-tutorials on web.</sub></b>

Hidden-page directly have meanings that should be available just for administrators (or service) team.

And this is looks like ToDo-list with entry-strings about some of things. 

Page in somewhat reason do not removed or (denied) after temporary-access-debug-time.


With this page we able to get more interesting (or helpful) information:
<ul>
<li>There is note "do not forget remove page or do deny access";</li>
<q><strong> ^ -> not completed there. so... maybe other things too.</strong></q>
<li>There is special URL for some of src-files, which also ask for credentials;</li>
<q><strong> ^ -> most likely there is can be "access-right"-check.</strong></q>
<li>There is note "do not forget re-change debug admin:admin credentials";</li>
<q><strong> ^ -> if page do not "disabled" - so maybe credentials too. </strong></q>
<li>There is note "do not forget update CMS-framework";</li>
<q><strong> ^ -> looks like that build of this CMS-framework was with known vulnerability;</strong></q>
<li>And some other entry-strings;</li>
</ul>
<pre>
 So after this result with found the hidden-page.
 And as additional potentially points with:
  -> debug credentials (admin:admin);
  which maybe do not changed.
 
  -> URL for page with some of src-files as review-ask other team 
      ( http:/127.0.0.1:8080/formsrc?review=on );
   which also covered by login-form.
   and probably have some of protection-layers;
 
  -> information about CMS Framework 
      (and that there was in use vulnerable build of this CMS);
   with this kind of project:
we will go to think that there is:
  known CMS and 
  known vulnerability for this CMS;
and design of vulnerability is:
  known "backdoor"-access credentials (as administrator-rights account);
Usually known vulnerabilities can be visible under the web:
  any websites, 
  cve-lists, 
  advisories and 
  other.
 
 So maybe this CMS Framework build also still not updated.
  "brief-search" for this vulnerability give the result that backdoor-credentials (CMS:CMSpassword).
</pre>

So, we have some information and able to try do something.

"src"-page covered by login-form (and looks like STRING-check under the parameter query by GET-method);

There is possible some steps: if "registered"-account will try to open this URL; anyone else; admin-account or some of tricks.

So we able to check if CMS Framework not updated and check "backdoor"-credentials from outdated build.

Open from "/hidden" page URL with "src"-files and get login-form.

Type there "CMS"-as-login and "CMSpassword"-as-password;

So we get access denied.... most likely there is check for something (but credentials are valid).

Go back to hidden page (and to src-review page after) or from login-form..

and try to use "admin:admin" for this special-src page.

Page is loaded and we get view of some src-file. Looks like html-template for some of pages.

<pre>
This page should be work as temporary storage for src-files as review-action by other team;

Most likely randomly page do not removed.
But mainly there is have some of "layers" of protection-access
(but not too much proper and valid for this situation);

So based on knowledge of admin-debug-credentials (from forgotten debug-page):
we able to review src of html-template file.
</pre>
<hr />

We can directly study this html-template src-file or will try to login and check what service able to do.

Stay opened src-file page and go open fresh tab with login-form.

And go to use any of already known for us credentials (admin:admin or CMS:CMSpassword).

Most likely there is can be other not strong passwords (by some of music band accounts).

But mainly (with current try) we able to think that music bands will use "strong" passwords.

But also able to think that "design" of handling this passwords can be with some troubles.

<pre>So with direct usage login-form for http://127.0.0.1:8080  and valid credentials</pre>

We able to get form-page like welcome-page.

      http://127.0.0.1:8080/form

There have ability to read information-words and invite listener (as music band's friend or other);

Go do "enter" from first! Ok, we get information that there is required name-field.

So fill it and we able do not fill "phone"-page. 

Or goes try to fill it (or both) with tricks like "html-tags or scripts"

So with this step <code>name</code> can be (as "alert" script usage): 

     <script>alert('name')</script>

And <code>phone</code> can be (as "alert" script usage):

     <script>alert('phone')</script>
     
Fill it and transfer to application.

We get result-page of this action, where information-words and menu with three URLs:

<ul>
<li> Add some else listeners;</li>
<li> Re-login;</li>
<li> And strange named URL</li>
</ul>
<hr />

<pre>
With this step we able back to known page with src-file.
And check it.

We able to found there potential trouble with handling output data from database about phones.

There visible that in somewhat reasons output text for phones comes as "unescaped text".
By the usage Thymeleaf (Java/HTML template engine) features.

Which time to time can be helpful - but not sure - that it can be helpful there.

Looks like that:
</pre>
        
       <td th:utext="${listener.phone}"><code>Listener phone</code></td>
    
<code>th:utext</code> probably comes there randomly (or for temporary debug);

This situation will create potential ability to do <strong>Cross-Site Scripting (XSS)</strong>

Name field have proper output handling as <code>th:text</code> (escaped text).

So.. with previous fill-action will be situation, when someone able to see list of listeners:

 -> there will be alert from "phone"-field (and visible "string" under the "name"-field).

But this troublepoint possible to use for any other actions and reasons.

Looks like that page with table of all listeners can be there....

Or just because it asked for review - maybe under the debugging.

-------

So back to the dreams about "strange named URL" under the "thanks-menu" after the transferring listener.

There have strange words as: <q><strong>Do you remember fylkr's song "do The Trick" from album "trick"?</strong></q>

and URL (page which can not be displayed) for 

<pre>http://127.0.0.1:8080/fylkr</pre>

We also able to find that under the "form-thanks" html-page (as src of page) for this URL/menu-tab have next strings:
           
           
      <div sec:authorize = "hasAuthority ('ADMIN')">

Which should means that current point have to be visible just for admins... but there is mistake with design.

So this is visible for all.

Most likely that there is can be else one temporary-debug or under-construction page.

And with knowledge that there is mistake and page can be there (and most likely strange words is tips):

 -> we able to start thinking around.

There was already some pages with "string"-checks under the GET-methods.

And looks like there is can be something around it.
We able to re-login under the admin credentials.

But because there is already mistake with check-about - so maybe page will be allowed to all too.

<pre>
We have potential debug-URL with debug-tips.

Words says about fylkr's song (and URL have /fylkr  page-name) song "do The Trick" from album "trick".
Go to think that there is tips how to do GET-query or how should be looks like URL for proper result.

After some tries... we able to get proper configuration for this:

http://127.0.0.1:8080/fylkr?trick=doTheTrick 
</pre>

If we open this URL after previous actions.. so we get firstly alert.

And after that full table (under the HTML template) with all invited listeners.
 <sub>(Donald Duck included, where "Donald" is name  and "Duck" is phone)</sub>

In fact - page should be visible just for administrators.

Looks like that there is just one protection-layer: GET / "parameter"-string from user's browser.

For this type of "hidden" page can be more protection in fact.


<hr />

MEANINGS
========

This project-application have some kind of troubles, vulnerable points and not proper usage design things.

All of this things (and tricks) will do ability to exploit it.

Mainly with this kind of "template/PoC" there missing too much critical exploiting or attack-points.

But this is anyway can be visible as "potential" troubles or things, which should be fixed.

Or which can be critical later...

Mainly there is next main troublepoints and additional troubles (which can be less likely exploiting or so visible):

<ul>
<li><code>debug-todo-page do not deleted or properly denied</code></li>
<br />
<li><code>page-for-administrators-only goes be protected just by get-parameter string</code></li>
<br />
<li><code>unescaped text output for phone-field</code></li>
<br />
<li><code>csrf-protection (provided by Spring framework) is disabled</code></li>
<br />
<li><code>so called "Powerful Custom CMS v2" with known vulnerability</code></li>
<br />
<li><code>passwords do not encrypted totally</code></li>
<br />
<li><code>HTTPS is missing</code></li>
<br />
<li><code>h2-console is available to be opened with this tries</code></li>
<br />
<li><code>do not added some of proper features</code></li>
<br />
<li><code>there is can be some of crash-situation for application</code></li>
</ul>

About first two points:
---
<pre>
this is already troublepoint... 
but also as result there start be visible a lot of other troublepoints.
like information, which can be critical start be randomly visible.

also list of all listeners (which should be just for administrators)...
goes be visible for all, who know proper string.
there is some of mistakes or not proper usage design 
(or just do not using proper design)...

so as result debug-page (with critical data) is available for all.

and page just for administrators:
do not protected by something more than get-query-string from user's browser.
</pre>

About unescaped/escaped text output and CSRF:
---
<pre>
phone-field with unescaped output text just do ability:
for exploiting situation by Cross-Site Scripting (XSS).
　
and mainly - if there will be more related troublepoints:
will be more higher risk-usage.
there is a lot of steps to prevent it (and mainly by frameworks in use - Spring or Thymeleaf);

by default (with proper usage) Spring Framework will add CSRF-protection enabled.
　
There is disabled-status for this feature under the security config.
　
But also do not "enabled" CSRF-protection (like tokens) under the html-templates.
　
So there is disabled and not enabled "CSRF-protection"..
but this is provided by tools in use for this project-application.
</pre>

About vulnerable "potential" CMS:
---
<pre>there is just "meanings" that this project-application using CMS.
　
And this CMS with known vulnerability (backdoor-admin-rights credentials).
　
And not updated properly... but current build of "this CMS" is "v5".
　
So.. too much outdated in fact. :) 
</pre>

About the other points:
---
<pre>
Passwords there is not encrypted. Not protected properly.
If there will be access to database (or hack it):
so it will be just passwords with normal view.

HTTPS is missing - so mainly:
there is can be visible all things between browser/application with less steps to do trick.

default console-access for build-in SQL/hibernate database is enabled:
and available to be opened with this tries.

there is a lot of features, which do not added yet:
Like "logout"-points and many other proper things.

design of some steps will create potential crash-situation. 
Time to time this is can be too much critical.
</pre>
<hr />
<hr />

<h1 id="owasp"><ins>Compare to OWASP Top TEN</ins></h1>

This project application can be vulnerable for some kind of attacks.
Or can be with vulnerabilities, troublepoints or mistakes.

Compare to OWASP and their Top Ten ( https://www.owasp.org/index.php/Top_10_2013-Top_10 ) there is can be next ones:

<b>Broken Authentication and Session Management</b> <strong>||</strong> <b>Sensitive Data Exposure</b>

  <pre>as OWASP A2 and OWASP A6</pre>

There is do not totally proper work with passwords (encryption or hashing is missing; and stored not encrypted passwords);

Missing encryption between application and browser. 

Do not handled logout and some other related things.

For fix this points - we able (as example) to use features, which provided by Spring Framework.

I add comments for project-application with places, which can be removed or added.

Mainly there we able to use "encryption"-methods for passwords and store it as encrypted ones (properly).

Good to use secure connection also. 

Also there is some kind of potential situation for "hack" password database.
<hr />

<b>Cross-Site Scripting (XSS)</b>

<pre>as OWASP A3</pre>

There is not really proper escaping for user input data. For one of forms (phone-field).

Which goes be under the table of all listeners.

For prevent it with current project-application:

we able to use "Thymeleaf" (Java/HTML template engine) with proper configuration about.

I also add comments about "potential" fix under the project-application.

Mainly there will be enough re-change "th:utext" to "th:text" under the fylkr.html-template.

So to use this troublepoint will be not so visible.
<hr />

<b>Security Misconfiguration</b>

<pre>as OWASP A5</pre>

This is main troublepoint for current project-application.

Start from this - we able to get some more things.

But there is already have some of critical (in common sense) things like:

default-debug admin credentials (admin:admin); 

unused debug pages with critical information ("/hidden"); 

unpatched tools in use ("potential" CMS);

default SQL/hibernate console is opened;

do not properly handling crash-situation;

some designs not properly used and other;

<hr />

<b> Missing Function Level Access Control </b>

<pre> OWASP A7</pre>

There is possible get visible information about "content, which not planned to be visible";

And also visible just use "user's browser" and action for get content, which should be covered.

Not enough check, protection-checks and some mistakes with design it.

Most of this places - I noted under the project-application.

There is possible do a lot of steps (different ones) and required to choose...

Usually this is based on "design" of application.

<hr />
<b> Cross-Site Request Forgery (CSRF) </b>

<pre>as OWASP A8</pre>

There is not properly designed CSRF-protection.

With current project-application there is not so many steps to critical-exploiting this.

But there is have possibilities around.

Mainly this is based on "csrf.disabled" feature.

For prevent it - we able use default security config feature by Spring Framework.

Or do additional check/protection under the templates (Spring/Thymeleaf) or another steps.

I added notes for project application about this places (mostly).

<hr />
<b> Using Components with Known Vulnerabilities</b>

<pre>as OWASP A9</pre>

For this project-application we able to think that there is some of "CMS" in use.

And this "CMS build" with known vulnerability.

Where is "known" backdoor-admin-account credentials.

CMS not updated and "account" not disabled.
<hr />
<hr />

<sub>
<strong>CyberSecurityCourse project-application for course series</strong>:
</sub>

<sub>
mooc.fi Cyber Security Base by University of Helsinki in collaboration with F-Secure Cyber Security Academy
</sub>
