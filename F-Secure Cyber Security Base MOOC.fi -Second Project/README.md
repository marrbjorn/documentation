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
       
 Most likely you normally able to use Packer/Vagrant/Metasploitable3/VMWare setting.
 ---
 ---
