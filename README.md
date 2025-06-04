# Dankium Browser
Dankium is a chromium based browser focused on providing top of the line security and adblocking in addition to other features.

## Android

### Features
* Memory Tagging Extension (Must be enabled on Android with advanced protection or developer options)
* Shadow Stacks
* Compiler Mitigations
* Adblocking
* Strong Android 13 Sandbox with minsdk bump
* External password manager first
* GPL 3.0 license to protect your rights
* much more

### Installing

To install from play store first join [Dankium Google Group](https://groups.google.com/g/dankium/).
Then join the [test program](https://play.google.com/apps/testing/app.dankium.browser) and it should appear in the [play store](https://play.google.com/store/apps/details?id=app.dankium.browser).

Alternatively you may download an apk for sideloading from [github releases](https://github.com/aroflcoppter/dankium/releases) but it won't automatically update so be sure to check back at least once a week if you don't know there's an update.

### Building

1. First clone the dankium repo and follow the [official instructions](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/android_build_instructions.md) with the dankium repo directory instead of making a chromium folder.
2. Make sure you download the entire history of chromium and refer back to this guide for modified steps.
3. Make sure you apply the patches while in the src directory with `git am --whitespace=nowarn --keep-non-patch ../patches/chromium/eyeo/*.patch && git am --whitespace=nowarn --keep-non-patch ../patches/chromium/hexavalent/*.patch && git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium/*.patch && git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium-noapikeys/*.patch`.
4. The proper gclient command is `gclient sync -D --with_branch_heads --with_tags --jobs 32` which is ran after checking out the right tag for the dankium build for example `git checkout 137.0.7151.72` in both the dankium folder and src folder.
5. Make sure you apply the angle patch `cd third_party/angle && git am --whitespace=nowarn --keep-non-patch ../../../patches/submodules/angle/*.patch && cd ../..`
6. When you run `gn args out/Default` be sure to paste in the contents of android_args.gn from the dankium repo.
7. Build with `autoninja -C out/Default chrome_public_apk` and your unsigned APK will be in out/Default/apks for installation with the option of signing first.
8. When you are updating make sure you pull both dankium and the src directories and checkout the right tag.

## Windows

### Features
* CET (Must have Windows 11 with compatible hardware)
* Compiler mitigations
* Adblocking
* GPL 3.0 license to protect your rights
* much more

### Installing

You may download an installer.exe from [github releases](https://github.com/aroflcoppter/dankium/releases) but it won't automatically update so be sure to check back at least once a week if you don't know there's an update.
You can use [API keys](https://www.chromium.org/developers/how-tos/api-keys/) from google as enviroment variables to sign into Dankium.

### Building

1. First clone the dankium repo and follow the [official instructions](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/windows_build_instructions.md) with the dankium repo directory instead of making a chromium folder.
2. Make sure you download the entire history of chromium and refer back to this guide for modified steps.
3. Make sure you apply the patches while in the src directory with `git am --whitespace=nowarn --keep-non-patch ../patches/chromium/eyeo/*.patch` and`git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium/*.patch` and optionally ` git am --whitespace=nowarn --keep-non-patch ../patches/chromium/dankium-noapikeys/*.patch` if you aren't gonna sign in.
4. The proper gclient command is `gclient sync -D --with_branch_heads --with_tags --jobs 32` which is ran after checking out the right tag for the dankium build for example `git checkout 137.0.7151.72` in both the dankium folder and src folder.
5. When you run `gn args out/Default` be sure to paste in the contents of windows_args.gn from the dankium repo.
6. Build with `autoninja -C out/Default mini_installer` and your mini_installer.exe will be in out/Default.
7. When you are updating make sure you pull both dankium and the src directories and checkout the right tag.

