Small background:
-----------------

This is more like "template" (or PoC), than "application" in fact.

    Design based on my too much small experience with all of this "development"-things;

Also I not really friendly with development.

So I decided to do not hard designed application and with some kind of "tricks" (as can be just like template-PoC);

-------

Project available at the github page: https://github.com/marrbjorn/CyberSecurityCourse

--> and <a href="https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-First%20Project">this page</a> will be as documentation of project;


Setup:
======
Get started can be with next steps:
-----------------------------------

<b>FIRST</b>: we have to be able work with https://cybersecuritybase.github.io (which means proper configured IDE and other requirements);

<br />
<strong>SECOND</strong>: download this project ( https://github.com/marrbjorn/CyberSecurityCourse ) as zip-file or by git-commands as usually.

<br />
<b>THIRD</b>: unpack it (if downloaded zip-file) and open project under the IDE (with Netbeans: "File -> Open Project..." under the menu).
   
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

Service provide ability to see full list of this listeneres.

    but this is should be available just for adminstrators (of party/service/website);
    
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
<ul>
=========

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

So we get access denied.... most likely there is check for something.

Go back to hidden page (and to src-review page) or from login-form..

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
to be continued....
