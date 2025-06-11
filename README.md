# Dankium Browser
Dankium is a chromium based browser focused on providing top of the line security and adblocking in addition to other features.
Please read and agree to the [Terms of Service](https://dankium.ca/tos.html) and [Privacy Policy](https://dankium.ca/privacy.html).

## Android

### Features
* Memory Tagging Extension (SYNC mode for highest protection against memory errors)
* Shadow Stacks
* Compiler Mitigations
* Adblocking
* Just-in-time compiled JavaScript and Web Assembly disabled to reduce attack surface
* Strong Android 13 Sandbox with minsdk bump
* External password manager first
* GPL 3.0 license to protect your rights
* No p2p webRTC to protect IP
* Disabled background sync to reduce attack surface
* much more

### Release Signing Key
The key is `contact@dankium.ca ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINZmfylHw5KGY3bgHr3wtnXAbx1gXifBZDfupD4RuCJ1` which you can also verify at the bottom of [dankium.ca](https://dankium.ca). The cert key for the apk is also `Signer #1 certificate DN: CN=aroflcoppter
Signer #1 certificate SHA-256 digest: dc52ec905e655c69602645c63ea41e82594d652d0d4b88f1ff7831d5f27da3b4
Signer #1 certificate SHA-1 digest: 0e246844630d81c2b4da2616756829f4677f5c9a
Signer #1 certificate MD5 digest: 1542441f5569f30f1d1cc75bbfcd5e09` and also at the bottom of [dankium.ca](https://dankium.ca).


### Installing

To install from play store first join [Dankium Google Group](https://groups.google.com/g/dankium/).
Then join the [test program](https://play.google.com/apps/testing/app.dankium.browser) and it should appear in the [play store](https://play.google.com/store/apps/details?id=app.dankium.browser).

Alternatively you may download an apk for sideloading from [github releases](https://github.com/aroflcoppter/dankium/releases) but it won't automatically update so be sure to check back at least once a week if you don't know there's an update.
You can verify the release before installation with `ssh-keygen -Y verify -f dankium_public_key -I contact@dankium.ca -n "Dankium Browser" -s Dankium.apk.sig < Dankium.apk` or on windows `cmd /c 'ssh-keygen -Y verify -f dankium_public_key -I contact@dankium.ca -n "Dankium Browser" -s Dankium.apk.sig < Dankium.apk'`provided you downloaded the public key.
There is a third method where you can use [obtanium](https://github.com/ImranR98/Obtainium) to update the sideloaded apk and check the signature but play store is prefered. 

### Building

1. First clone the dankium repo and follow the [official instructions](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/android_build_instructions.md) with the dankium repo directory instead of making a chromium folder.
2. Make sure you download the entire history of chromium and refer back to this guide for modified steps.
3. Make sure you apply the patches while in the src directory with `git am --whitespace=nowarn --keep-non-patch ../patches/chromium/eyeo-dankium/*.patch && git am --whitespace=nowarn --keep-non-patch ../patches/chromium/hexavalent/*.patch && git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium/*.patch  && git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium-noapikeys/*.patch`.
4. The proper gclient command is `gclient sync -D --with_branch_heads --with_tags --jobs 32` which is ran after checking out the right tag for the dankium build for example `git checkout 137.0.7151.72` in both the dankium folder and src folder.
5. Make sure you apply the angle patch `cd third_party/angle && git am --whitespace=nowarn --keep-non-patch ../../../patches/submodules/angle/*.patch && cd ../..`
6. Also make sure you apply the libunwind patch `cd third_party/libunwind/src && git am --whitespace=nowarn --keep-non-patch ../../../../patches/submodules/libunwind/*.patch && cd ../../..`
7. When you run `gn args out/Default` be sure to paste in the contents of android_args_*.gn for the target processor from the dankium repo.
8. Build with `autoninja -C out/Default chrome_public_apk` and your unsigned APK will be in out/Default/apks for installation with the option of signing first.
9. When you are updating make sure you pull both dankium and the src directories and checkout the right tag.

## Windows

### Features
* CET (Must have Windows 11 with compatible hardware)
* Compiler mitigations
* Adblocking
* Just-in-time compiled JavaScript and Web Assembly disabled to reduce attack surface
* GPL 3.0 license to protect your rights
* No p2p webRTC to protect IP
* Interpreted only JavaScript to reduce security risk
* Disabled background sync to reduce attack surface
* much more

### Installing

You may download an installer.exe from [github releases](https://github.com/aroflcoppter/dankium/releases) but it won't automatically update so be sure to check back at least once a week if you don't know there's an update.
You can verify the release before installation with `ssh-keygen -Y verify -f dankium_public_key -I contact@dankium.ca -n "Dankium Browser" -s Dankium_Installer.exe.sig < Dankium_Installer.exe` or on windows `cmd /c 'ssh-keygen -Y verify -f dankium_public_key -I contact@dankium.ca -n "Dankium Browser" -s Dankium_Installer.exe.sig < Dankium_Installer.exe'`provided you downloaded the public key.
You can use [API keys](https://www.chromium.org/developers/how-tos/api-keys/) from google as enviroment variables to sign into Dankium.

### Building

1. First clone the dankium repo and follow the [official instructions](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/windows_build_instructions.md) with the dankium repo directory instead of making a chromium folder.
2. Make sure you download the entire history of chromium and refer back to this guide for modified steps.
3. Make sure you apply the patches while in the src directory with `git am --whitespace=nowarn --keep-non-patch ../patches/chromium/eyeo-dankium/*.patch` and`git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium/*.patch` and if you are not gonna provide apikeys `git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium-noapikeys/*.patch`.
4. The proper gclient command is `gclient sync -D --with_branch_heads --with_tags --jobs 32` which is ran after checking out the right tag for the dankium build for example `git checkout 137.0.7151.72` in both the dankium folder and src folder.
5. When you run `gn args out/Default` be sure to paste in the contents of windows_args_*.gn for the target processor from the dankium repo.
6. Build with `autoninja -C out/Default mini_installer` and your mini_installer.exe will be in out/Default.
7. When you are updating make sure you pull both dankium and the src directories and checkout the right tag.

## Credits
* [aroflcoppter](https://github.com/aroflcoppter/dankium/blob/main/LICENSE)
* [the chromium authors](https://chromium.googlesource.com/chromium/src/+/HEAD/LICENSE)
* [eyeo](http://github.com/aroflcoppter/dankium/blob/main/patches/chromium/eyeo-dankium/LICENSE)
* [flawedworld](https://github.com/aroflcoppter/dankium/blob/main/patches/chromium/hexavalent/LICENCE)
