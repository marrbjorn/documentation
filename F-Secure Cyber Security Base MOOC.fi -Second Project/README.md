###### CONTENTS
* ##### [Tries to set up Metasploitable 3 --with previous CSB launch--](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-Second%20Project#tries-to-set-up-metasploitable-3);
* ##### [SNORT --with previous CSB launch--](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-Second%20Project#snort);
* ##### [Metasploit --with previous CSB launch--](https://github.com/marrbjorn/documentation/tree/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-Second%20Project#metasploit);
* ##### [FRESH additions based on Cyber Security Base course series 2017 --CSB-2017--](https://github.com/marrbjorn/documentation/blob/master/F-Secure%20Cyber%20Security%20Base%20MOOC.fi%20-Second%20Project/README.md#csb-2017);

# Tries to set up Metasploitable 3 (with previous CSB launch).

With Project TWO ( https://cybersecuritybase.github.io/project2/ ) we have to install vulnerable system (Metasploitable 3).

And expected option - do this by VM (as example - VirtualBox);
    
    I uninstalled VirtualBox some time before (based on a lot of crashes and troubles);
    And replaced it with VMWare Player.

Instruction-steps and requirements are available Under the Metasploitable3 wiki-page.

    System Requirements:
    ====================
    # OS capable of running all of the required applications listed below
    # VT-x/AMD-V Supported Processor recommended
    # 65 GB Available space on drive
    # 4.5 GB RAM
    
    Requirements:
    =============
    # Packer
    # Vagrant
    # Vagrant Reload Plugin
    # VirtualBox
    # Internet connection
    
For me it means that there are small options to launch current VM (not enough powerful Linux machine and not possible under VMWare Player).

<h3><strong>FIRST TRY</strong></h3>
I decided to try common workaround steps with one of Windows machines (with partly enough hardware configuration).

Also, I found under metasploitable3-folder that we can to use .json-file for VMWare.

So, I tried to use it.

Installation of Packer is quite normal and brief-step (also I manually added it to system PATH).

Vagrant installation is also quickly and added to system PATH by installation-steps. 

Reload plugin is also normally installed by documentation-steps.

But brief-try to use it with VMWare Player shows mistakes (VMWare PLAYER is not supported).

Even it was possible to fix some parts of trouble (add some folders to the PATH; get the VMWare VIX and some of plugins/addon-files).

All of this fix-resources are available on VMWare website/kb-pages. And under Vagrant documentation (like plugin for VMWare).

These steps are required only for tries to use Vagrant and VMWare Player. And workaround was close to proper view.

But based on another "limitation" of use (I thought that it is licence-ask about VMWare) - I decided to try VMWare Workstation Pro (trial-time) - what if it will be more good and work from first.

With VMWare Workstation PRO (trial-time); .json-file (metasploitable3) for VMWare; also with Packer/Vagrant usage - there is quite good result (potentially). And all should work....

But I found that noted "licence-ask" (when we will try to add Vagrant box to the VM) is about certain Vagrant design.

If we want to use Vagrant and VMWare (supported VMWare Workstation) - we have to buy licence "Vagrant VMWare".

So... maybe it is OK, but during my try - their "shop" was not available anyway. Payments methods are not visible and just missing.

Thus, I removed VMWare (and uninstalled vagrant plugin for vmware-workstation). And start to try next option-step.

<strong>Main meanings about this try:</strong>

&#8608; If you have (or do able to buy) Vagrant VMWare licence (another licence than just VMWare licence);

&#8608; And you are owner of licence for the VMWare Workstation (or maybe other supported solutions);

       or optionally do able to do some workarounds for VMWare Player with not expected result.
       
<strong>Most likely you are able to use Packer/Vagrant/Metasploitable3/VMWare setting.</strong>

 ---
 ---
 
 <h3><strong>SECOND TRY</strong></h3>
 
 I installed VirtualBox (latest build).
 
 Then with already installed and configured (before this) Packer/Vagrant:
 
 I tried to use packer build with related metasploitable3 .json-file.
 
 As result : stuck for SSH-waiting.
 
     ==> virtalbox-iso: waiting for SSH to become available...
     
 After some time (hours maybe) time-out is comes and break the process.
 
 This step is also take delay with my VMWare experience but anyway with normal result.
 
 So, I decided to re-run it with Virtualbox else one time. But also troubleresult after hours.
 
 Basically, at first there was resource-usage but then "not" and just stuck for SSH-waiting.
 
 Some thoughts and else one run - anyway stuck.
 
 I decided to re-check situation with editing .json-file;
 
 I re-change headless-option for VirtualBox running from default-configuration to:
 
      "headless": false
      
 And with my experience - looks like - that waiting for boot up (just two minutes) is not enough.
 
 At least, when commandline with already noted waiting for SSH (shortly after the waiting for boot up):
 
 there is still installation process about first of steps.
 
 When installation completed and scripts are launched under the VM-command line there was visible:
 
 that with try to do something about SSH - comes a lot of mistakes as output. 
 
 Not check it more because decided to try add more "boot-time waiting" and check the result else one time.
 
 what if "ssh"-scripts launched with time when it is not expected and 're-launch' is not work with proper time.
 
 So... I added some time for "boot up waiting"-option (seven minutes).
 
 AND probably it is not really related with my situation. There anyway was delay between this commands/results.
 
 And, most likely, "ssh"-scripts launched anyway ("re-launch" work - if the boot was with delay).
 
 Because system is launched and anyway was a lot of mistakes with ssh-cmd-line action (not sure what it was there).
 
 I decided to check more with system "UI". Re-check Firewall rules, re-check folders.
 
 There was missing SSH-clients (OpenSSH folder). I decided that maybe it should be there.
 
 Mainly because there was Firewall rules for such destination.
 
 Go to the VM's browser, Google and type OpenSSH (I am not really friendly with ssh).
 
      also there was troubles with opening some HTTPS pages.
      metasploitable3 about outdated build of Windows.
      and looks like there is Internet Explorer 8.
      
      So, I start to think at this step.. that maybe there is trouble about such.
      If websites/changes for HTTPS-setting goes be with broken work under this system...
      some scripts-download/get OpenSSH or other requirements may not work too.
      
 Found also that OpenSSH website is not about Windows platform.
 
 And for Windows usage should be available next URL (and packages there):
 
     https://www.mls-software.com

Then, I got notification about "page is not available" (based on HTTPS).

Re-change protocol to HTTP and got blockpage by F-Secure. :)

    I have to add that my main system (where I try to set up metasploitable3) with F-Secure SAFE installation.
    
    F-Secure SAFE - F-Secure security solution for home users. With two modules AV and Browsing Protection.
    
    Browsing Protection is not about just blocking harmful pages and suspicious-rated pages.
    
    But also there are some features like Content Blocker (mainly as Parental Control feature).
    
    I use Content Blocker for "restrict" access to "unknown-content" pages. 
    
    As result F-Secure installation will block all pages which unrated (unknown/uncategorized) by F-Secure yet.
    
And this mls-software page is certainly this unrated page by F-Secure (on current time/day).

Funny point that F-Secure is installed under my main system but also will block (restrict access) under VM's system/browser.

Maybe good.

So, it was already more visible that maybe it can be a reason for SSH-stuck (downloading openssh just not started as example).

I turn off Content Blocker feature. And run next try (packer build).

Yes, SSH is normally started and further process goes be with good view.

BUT.... result comes with some of fresh stuck-points (already second time) and as result:

    ==> Builds finished but no artifacts were created.
    
So, I have to try some checks about situation and understand what can be stuck-reason with this time.

Lines about potential troubles with not visible reason yet (for me). 
 
Fresh stuck was about next strings-result:

    ==> Some builds didn't complete successfully and had errors:
    --> virtualbox-iso: Error removing floppy controller: VBoxManage error: 
    VBoxManage.exe: error: The machine 'packer-virtualbox-iso' is already locked for a session (or being unlocked)
    VBoxManage.exe: error: Details: code VBOX_E_INVALID_OBJECT_STATE (0x80bb0007), 
    component MachineWrap, interface IMachine, callee IUnknownVBoxManage.exe: error: 
    Context: "LockMachine(a->session, LockType_Write)" at line 1038 of file VBoxManageStorageController.cpp
    
Firstly I tried to search about this lines.

As result I got view that a lot of people get time to time this troublepoint.

And practically each situation with not visible fix (potentially some different workarounds for them).

I start to think that maybe my situation is about something else (because some points with differences).

Also worst point of situation:

    usually about troublepoints with Packer/Vagrant (?) - there tries to say that trouble with Windows.
    but most of users noted that situation and troublepoints are not related with Windows at all.
    At least, for common view of this.
 
I decided to check if just "restart" for my main system will be enough.

Because thought - what if my a lot of tries to do "packer build" triggered stuck for VirtualBox or other things.

I did the restart. I re-run packer build and it normally completed!

Also, I normally added "box" to vagrant.

Next step is "vagrant up"..

With some of check-steps vagrant up is normally started but stable-stuck with trouble result about next point.

    http://sourceforge.mirrorservice.org/w/wa/wampserver/WampServer 2/WampServer 2.2/wampserver2.2d-x64.exe
     
In somewhat reason this URL will return "Page not found" (this URL from scripts).

As result, "vagrant up" do not able complete process normally. Wampserver is not installed.

So - I am not sure - why this URL is troublepoint with my experience.

Looks like that it is stable "Page Not Found".

So, it should be known trouble - but I did not find something about it (briefly).

Thus, I decided just create changes for "metasploitable3\scripts\installs" about install_wamp.bat


    Re-change this trouble-URL:
    -> http://sourceforge.mirrorservice.org/w/wa/wampserver/WampServer 2/WampServer 2.2/wampserver2.2d-x64.exe
    to next URL: 
    -> https://downloads.sourceforge.net/project/wampserver/WampServer 2/WampServer 2.2/wampserver2.2d-x64.exe
    under the related string-line of .bat-file

Re-check with fresh "vagrant up" and all downloaded/installed (at least - this step is already not a stuck-point);

&#8688; Probably process is completed and looks like that I have to try launch VirtualBox.

But with my first experience was maybe known trouble about VirtualBOx VMs stuck;

I can to think about some of tries - most likely most of them can be helpful.

But with my experience was enough just restart my main system.

After this - I launched configured VirtualBox VM. 

Some further configure-steps for system and I tried to download Snort with their rules.

And got total stuck about this step (but mainly with downloading rules). It was not available.

With next day - I randomly met notification that probably during certain time there was troubles with Amazon S3.

Most likely (and looks like) this trouble was about time when I tried get Snort-rules.

And snort-rules are certainly about s3.amazon-URLs, which was not available.

I tried download rules today and all OK, good and normal. So, most likely it was related with this "trouble".

    This situation (with amazon-s3) under articles marked as critical and large trouble.
    But with my experience - I totally do not feel it. 
    I just randomly get trouble-stuck with downloading Snort-rules.
    BUT ALSO MAYBE with uploading files to the github.com; I tried two picture-files.
    It was stable with "trouble"-result. Today - all OK with related steps.
    
    And this experience was more random than common for my usage. 
    So, yes, it was large trouble, but not so critical.

Just anyway good to use such things with reasonable points and with places where indeed it required too much.
<hr />

Most likely "set up" is completed. So, will play with Snort.

# SNORT (with previous CSB launch)

Firstly tried to understand how to properly use Snort and which result there should be.

Decided to set up it as third "option" : Network Intrusion Detection System Mode ;

With this step (NIDS-try) I got trouble-stuck about configuration.

On current time about next one:

    ... Missing/incorrect dynamic engine lib specifier. Fatal Error, Quitting ...

Some tries, some search with web... but result anyway about this stuck.

Will play with Snort more.... 

stuck mainly was about "uncomment"-action for "outdated" rules together with updated-rules.

Thus, I re-check/re-fix and add some else changes to snort.conf (I mean - not just expected ones).

Launch snort and maybe it work as IDS; logs also there.

But I have to re-check about certain settings/set-up for good result of Snort-work.

So, before experience with metasploit - I have to "play" with Snort more time.

Still not sure that snort is configured with enough view/setting and that there is expected set-up.

After some days - I configured Snort maybe with "OK"-view.. 

But with my try to scan ports (and get information about results) - Snort ignore it (or some kind of);

Will try to check more about Metasploit and Snort possibilities.

But found that I am not able to download Metasploit. So will play else one time... with this already.

After some tricks and tweaks looks like that I am able to use Metasploit.

So, if SNORT do able to detect such things (which most likely required some else steps :( and configuration):

I already able to start trying to play with Metasploit more time.

Will be interesting..

# Metasploit (with previous CSB launch)

So, based on my set-up I had to re-improve snort.conf and add some of limitations, exceptions, advanced rules to my setting.

By "setting" I mean full meanings of this Course Project Two (as configuration of system, VMs, Metasploit and Snort).

And this is not really quite good and not common situation. Mostly it should be more properly - if it indeed planned to be in use.

But, anyway, one of example-reasons for re-improve situation (with not totally change full setting):

&#8692; in somewhat reason I tried Metasploit Community (with Pro Trial probably experience will be more friendly).

as result some of additional steps and more "time" for getting knowledge about proper use.

======

After some time, tries, researches and actions - I got and understand some examples of Snort good detection work.

But also about certain situations when Snort do not trigger something helpful.

As result - there more thoughts about reasonable points of using both "tools":

&#8692; Metasploit;

&#8692; Snort.

And basically with both of them there are a lot of abilities do (or not to do) different things.

....

# CSB-2017

So, today decided to set up Metasploitable3 for **current launch (second) of cybersecuritybase**.

It takes seven hours. One hour about research and troubleshoot fresh stuck points.

Firstly, I decided to try another machine and system. As result, fresh tweaks like:

- changes to system own configuration (proper support VM);
- changes to installed software configuration (allowing disabled restricted content URLs);

Then was large stuck about next step:

    powershell -Command "(New-Object System.Net.WebClient).DownloadFile 
    ('https://github.com/downloads/alexkasko/openjdk-unofficial-builds/openjdk-1.6.0-unofficial-b27-windows-amd64.zip',
    'C:\Windows\Temp\openjdk-1.6.0-unofficial-b27-windows-amd64.zip')
    "Exception calling "DownloadFile" with "2" argument(s): 
    "The request was aborted: Could not create SSL/TLS secure channel."
    At line:1 char:1+ (New-Object System.Net.WebClient).DownloadFile('https://github.com/do ...+ + 
    CategoryInfo          : NotSpecified: (:) [], 
    MethodInvocationException    + FullyQualifiedErrorId : WebException

Such direct URL was with troubles to be opened even with Internet Explorer 11 (but not with InPrivate mode);

Some tries to re-check what is it (to enable all TLS under settings; switch rules for zones; other tweaks).

Found that after all changes and with disabled SmartScreen - URL is opened good with Internet Explorer 11. 

But anyway with trouble result during scripts (powershell). Sounds that TLS1.2 is needed.

Tries to re-check about reason and I decided to use/create such changes to .bat-file like workaround-fix:

Fix:

    powershell -Command "[Net.ServicePointManager]::SecurityProtocol = 'tls12, tls11, tls'; (New-Object System.Net.WebClient).DownloadFile('https://github.com/downloads/alexkasko/openjdk-unofficial-builds/openjdk-1.6.0-unofficial-b27-windows-amd64.zip', 'C:\Windows\Temp\openjdk-1.6.0-unofficial-b27-windows-amd64.zip')" <NULcmd /c ""C:\Program Files\7-Zip\7z.exe" x "C:\Windows\Temp\openjdk-1.6.0-unofficial-b27-windows-amd64.zip" -oC:\openjdk6"
    
So, stuck is sorted. Then one-time manual restarting VM and, as result, all configured and possible to use.

Then was play (else one time) with Snort (still Snort 2* /2.9.11.1/). I thought that after my previous experience it will be more brief-step.

But not. I decided to use Windows 10 machine with this launch too. Snort and Windows - pretty strange for configure.

I tried to tweak most of things for good state from first. But got some stuckpoints for research.

In general, some of them was with previous launch too (I did not 'remember' them).

All of them well-known and even discussed with Snort Support/Mailing lists. But unclear why it is not listed under documentation.

Then - why config is not about any tips for most popular troubles. Even there is Pulledpork (I did not try it - but sounds as solution).

But with this CSB-launch -> snort configuration take less time. Even it is still pretty good to tweak a little be.

I decided to install Metasploit next and got some unexpected troubles. Three reinstallation for got proper view.

Brief try with play around Metasploit and probably good to start play with full stack: Metasploitable3, Snort and Metasploit.

But got an unexpected trouble with Metasploit; tries to research, fix or so - but else one reinstallation.

Decided to tweak entire stack and, as result, received strange situation with both of them.

Strange results with Metasploit, strange results with Snort.. did not play enough.

In fact, performed most of important things - but I thought that I will play more...

So, I have to re-check situation with more time and then will be possible to play more.

...
