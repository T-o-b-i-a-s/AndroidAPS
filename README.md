# AndroidAPS with autoISF
* For documentation about AndroidAPS without autoISF, check the wiki:
  https://androidaps.readthedocs.io
* Everyone who’s been looping with AndroidAPS needs to fill out the form after 3 days of looping
  https://docs.google.com/forms/d/14KcMjlINPMJHVt28MDRupa4sz4DDIooI4SrW0P3HSN8/viewform?c=0&w=1

## What is autoISF?
AutoISF adds more power to the algorithm used in AndroidAPS by adjusting the insulin sensitivity
based on different scenarios (e.g. high BG, accelerating/decelerating BG, BG plateau).
autoISF has many different settings to fine-tune these adjustments.
However, it is important to start with well-tested basal rate and settings for insulin sensitivity
and carb ratios.

## Where to find documentation about autoISF
* Please visit ga-zelle’s repository [GitHub - ga-zelle/autoISF](https://github.com/ga-zelle/autoISF/tree/A3.4.2.6_ai3.2.1).
* This repo contains a [ReadMe document](https://github.com/ga-zelle/autoISF/blob/A3.4.2.6_ai3.2.1/README.md) with a description of the latest changes to AutoISF
* The [**Quick Guide (bzw. Kurzanleitung)**](https://github.com/68d23e02-a816-45de-83ad-d5483ef5e351) provides an overview of autoISF and its features


## Why do I get AutoISF here and not at ga-zelle's Repo?
* The vast majority of the AutoISF design and development effort was done by
  [ga-zelle](https://github.com/ga-zelle) with support from
  [swissalpine](https://github.com/swissalpine), [claudi](https://github.com/lutzlukesch),
  [BerNie](https://github.com/bherpichb), [mountrcg](https://github.com/mountrcg),
  [Bjr](https://github.com/blaqone), [Gohtraw](https://github.com/Gohtraw),
  [Koelewij](https://github.com/koelewij) and [myself](https://github.com/T-o-b-i-a-s).
* This repository here was created to provide a stable version of AndroidAPS with the current
  autoISF extensions already integrated to simplify the build process.
* This branch https://github.com/T-o-b-i-a-s/AndroidAPS/tree/3.4.2.6+aisf3.2.1 uses
  [AndroidAPS 3.4.2.6](https://github.com/nightscout/AndroidAPS/releases/tag/3.4.2.6)
  from the official [Nightscout AndroidAPS](https://github.com/nightscout/AndroidAPS)
  repo as a base and adds autoISF 3.2.1 to it.

## Why was autoISF not part of the official AndroidAPS "master" version?
* With AndroidAPS 3.3, autoISF was introduced as a plugin, but can only be enabled in dev mode
* The version available here makes the latest 3.2.1 version of autoISF available in the currently  
  latest 2.4.2.6vAndroidAPS version even without dev mode

# Building
## How to build this branch within the Browser (Github Actions)
1. Sign in to Github, or [create a new Github Account](https://github.com/signup) if you do not
   have one yet
2. Create a fork of this repo in your own account by pressing the "Fork" button. When asked, click
   the checkbox to "Copy the `3.4.2.6+aisf3.2.1` branch only".
   If you get the error message "No available destinations to fork this repository.",
   you probably already have a fork of AndroidAPS. Github does not allow two forks of the same
   base repository. You now have two options:
    * __Simple__: If you do not know how to use the `git` command line tool and forking this repo does not
      work, you can create a clone of a [forkable copy of this repo](https://github.com/T-o-b-i-a-s/AndroidAPS-autoisf-clonable),
      however you will then need to create your Github repository secrets again for this repo to be
      able to use the browser build.
    * __Advanced__: If you are familiar with the `git` command line tool on your PC, you can use it to add this
      repository as a second remote, checkout this branch locally and push it to your already
      existing AndroidAPS repository. This will allow to reuse any existing Github repository secrets
      already created for using the browser build functionality for the official AndroidAPS version.
3. If you have never used the browser build before or you have used the forkable copy to create
   your fork, now follow the [preparation steps](https://androidaps.readthedocs.io/de/latest/SettingUpAaps/BrowserBuild.html#preparation-steps)
   to create secrets within your forked autoisf Repository. Make sure the secrets are created within
   the repository that contains this autoisf branch. This is a one time step to setup the browser
   build and can be skipped if you already did it earlier.
4. Now start the browser build using the Github Action
   [aaps-ci](https://androidaps.readthedocs.io/de/latest/SettingUpAaps/BrowserBuild.html#aaps-ci-github-actions-to-build-the-aaps-apk).
   At the moment when the description asks you to select the "master" branch, make sure to
   select this branch "3.4.2.6+aisf3.2.1" when setting the parameters to really create AndroidAPS
   with autoISF included.
5. After the build is completed, you can download the APK from your Google Drive that was used when
   setting up the Github repository secrets in step 3

## How to build this branch in Android Studio
1. Get the latest version of Android Studio
2. Close any currently open projects in Android Studio
3. Create a new project by using the "Get from VCS" button to tell it to retrieve the source from a
   remote version control system
4. Use the url of this repository as a source (https://github.com/T-o-b-i-a-s/AndroidAPS.git).
   Do **NOT** append any branch name or version number or other path, **just use the URL as
   shown above**!
5. Now wait until Android has completed any initialization activities. As always deny any requests 
   to upgrade Gradle. A "Gradle sync" might however be necessary.
6. Android Studio now shows the name of the current branch on the upper left within the title bar.
* This will often be `master`, which contains a version of AndroidAPS without autoISF,
  do **not** use the `master` branch
* If it is not already selected, switch to the branch you want to build by clicking on the branch
  name, choosing "show more" under "Remote branches" and look for the name of
  the branch with an "origin/" prefix: e.g. `origin/3.4.2.6+aisf3.2.1`. Left-click that name and
  select "Checkout".
7. The system will now create a local branch with the same name as the remote branch and switch to that branch, which is indicated by the name of
   the branch being shown in the upper right corner
8. You can now build the APK with Build -> Generate signed Bundle / APK
9. If you get an error about an incompatible JVM or Java Version, read the troubleshooting section within the official
   [AndroidAPS documentation](https://androidaps.readthedocs.io/en/latest/GettingHelp/TroubleshootingAndroidStudio.html#incompatible-gradle-jvm)
10. In case of any error messages during the build, try to first run a "Clean build" by selecting
    Build -> Clean to remove any remnants from previous builds and then start the APK build again.
11. If you experience recurring problems with building the APK, as a last resort consider to
    delete your current Android Studio completely, reinstall the most recent version and clone
    this repo into a new directory on your computer (different than the one you have used before).

### What can I do if the build does not work?
* Follow the instructions exactly as described. Carefully re-read all previous and the failing
  step and try to start from scratch.
* Make sure you used "https://github.com/T-o-b-i-a-s/AndroidAPS.git" as the URL to "Get from VCS"
  and none including the branch or version name
* If you have problems understanding English and need a translation, consider using an automatic
  translation tool such as https://www.deepl.com where you have to copy and paste the english text
  to get it translated or use [Google Translate](https://github-com.translate.goog/T-o-b-i-a-s/AndroidAPS?_x_tr_sl=en&_x_tr_tl=de&_x_tr_hl=de&_x_tr_pto=wapp)
  to automatically translate the whole page (target language is set to German in this example, but can be changed at the top).

General remark:
If you have been working with older AndroidAPS versions (2.x, 3.0, 3.1, 3.2, 3.3) before and this is the first time you build a 3.4 version,
please first build and run the regular AndroidAPS 3.4.x version from
https://github.com/nightscout/AndroidAPS and double-check that this works fine.
Only then upgrade to the version including autoISF.

For questions or feedback, please contact us at https://de.loopercommunity.org/t/woher-wie-autoisf/
