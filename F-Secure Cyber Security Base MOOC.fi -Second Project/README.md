# Tries to set up Metasploitable 3.

With Project TWO ( https://cybersecuritybase.github.io/project2/ ) we have to install vulnerable system (Metasploitable 3).

And expected option - do this by VM (as example - VirtualBox);
    
    I have uninstalled VirtualBox some time before (based on a lot of crashes and troubles);
    And re-place it with VMWare Player.

Under the Metasploitable3 wiki-page available instruction-steps and requirements.

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
    
For me it means that there is small options to launch current VM (not enough powerful Linux machine and not possible under the VM machine).

#FIRST TRY
So I decided to do this by common steps with one of Windows machine (around normal settings).

Also I found that under the metasploitable3-folder we can to use .json-file for VMWare.

I did the try to use it.

Installation of Packer quite normal and brief-step (also added this to system PATH).

Vagrant installation also quickly and added to system PATH by installation-steps. 

Reload plugin also normally installed by documentation-steps.

So brief-try to use it for the VMWare Player shows mistakes (not supported VMWare Player).

But it was possible to fix about some of troubles (add some folders to the PATH and get the VMWare VIX and some of plugins/addon-files).

All of this resources available from VMWare website/kb-pages. And under the Vagrant documentation (as plugin for VMWare).

This steps mainly required just for trying use Vagrant for the VMWare Player. And workaround was around proper view.

But based on other "limitation" (I thought that license-ask about VMWare) - I decided try VMWare Workstation Pro (trial-time) - if it will be more good and work from first.

With VMWare Workstation PRO (trial-time) and .json-file (metasploitable3) for VMWare under the Packer/Vagrant usage - there is quite good result.

But I found that "license-ask" (when we will try to add Vagrant box to the VM) about certain Vagrant design.

If we want to use Vagrant and VMWare (supproted VMWare Workstation) - we have to buy license "Vagrant VMWare".

Maybe it OK, but during my try - their "shop" was not available anyway. Payments methods not visible and just missing.

So - I remove VMWare (uninstall vagrant plugin for vmware-workstation also). And start try next option-step.

<strong>Main meanings about this try can be like that:</strong>

--> If you have (or able to buy) Vagrant VMWare license (different with just VMWare license);

--> And you have license for the VMWare Workstation (or maybe officially supported some other solutions);

       or optionally able to do some of workarounds for VMWare Player with not expected result.
       
<strong>Most likely you normally able to use Packer/Vagrant/Metasploitable3/VMWare setting.</strong>
 ---
 ---
 
 <h3><strong>SECOND TRY</strong></h3>
 
 I installed VirtualBox (latest build).
 
 And with already installed/configured (before this) Packer/Vagrant:
 
 I did the try to use packer build for the related metasploitable3 .json-file.
 
 As result : stuck for SSH-waiting.
 
     ==> virtalbox-iso: waiting for SSH to become available...
     
 After some time (hours maybe) time-out comes and break-the-proces.
 
 This step also take some delay with my VMWare experience, but anyway normally work.
 
 So, I decided to re-run this for Virtualbox else one time. But the same result after hours.
 
 Basically there was resource-usage, but after that "not" and just stuck for SSH-waiting.
 
 Some thought and else one run - anyway stuck.
 
 I decided to re-check situation with editing .json-file;
 
 I re-change headless-option for VirtualBox running from default-configuration to:
 
      "headless": false
      
 And with my experience - looks like that there is waiting for boot up (just two minutes) not enough.
 
 At least - when command line already noted waiting for SSH to become available (shortly after the waiting for boot up):
 
 There is still installation process about first of steps.
 
 When installation comes and scripts launched under the VM-command line there was visible:
 
 that with try to do something about SSH - there comes a lot of mistakes as output. 
 
 Not check it more - because decided to try add more "boot-time waiting" and check the result else one time.
 
 What if the "ssh"-scripts launched with time, when it not expected and not work "re-launch it" with proper time.
 
 So... there is will be result soon.
 
 
 
 
