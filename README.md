# Swift Style

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
![Platforms](https://img.shields.io/badge/platform-iOS-lightgrey.svg)
[![Swift Version](https://img.shields.io/badge/Swift-5.7-orange)](https://developer.apple.com/swift)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![Twitter](https://img.shields.io/badge/twitter-quantum__tunnel-blue)](http://twitter.com/quantum_tunnel)
[![BioSite](https://img.shields.io/badge/BioSite-jrogel-blue)](https://bio.site/jrogel)
[![Website](https://img.shields.io/badge/web-jrogel-black)](https://jrogel.com)
[![Website](https://img.shields.io/badge/web-RogueLoop-black)](https://rogueloop.jrogel.com)

This repo contains information used to configure [SwiftLint](https://github.com/realm/SwiftLint). These guides use SwiftLint as a standard. You can learn more about SwiftLint by visiting its [official documentation page](https://github.com/realm/SwiftLint).

## Table of Contents

* [Installing SwiftLint](#installing-swiftlint)
* [Using the configuration file](#using-the-configuration-file)
* [Xcode settings](#xcode-settings)
* [Running SwiftLint](#running-swiftlint)
* [Handling rule exceptions](#handling-rule-exceptions)

## Installing SwiftLint

You can easily install SwiftLint using Homebrew:

```bash
brew install swiftlint
```

If you are unable to use Homebrew, you may use one of the other methods described in the [SwiftLint documentation](https://github.com/realm/SwiftLint).

## Using the configuration file

To facilitate the use of the configuration file I do not place it in the project folder as suggested in the documentation. Instead I place it in a known directory (e.g. home). 

## Xcode settings

In the Xcode configuration I am using the option to remove trailing whitespace from all lines. 

## Running SwiftLint

You can run SwiftLint in your project by following these steps:

1. Select the project document in the Project navigator.
1. Select the **Build Phases** tab.
1. Click **+** and choose **New Run Script Phase**.
1. Drag the new phase before the **Compile Sources** phase.
1. Click the disclosure triangle on the **Run Script** phase and ensure **Shell** is set to **/bin/zsh**.

6. Add the following script:
```zsh
export PATH="$PATH:/opt/homebrew/bin"
if which swiftlint >/dev/null; then
    for yml in ~/rogelj.swiftlint.yml
    do
        if [ -f $yml ]; then
           swiftlint --no-cache --config $yml
            break
        fi
    done
else 
    echo "warning: SwiftLint not installed, download from https://github.com/realm/SwiftLint"
fi
```

Please note that if you decide not to use the configuration file in this repo (or any) it is possible to use the default configuration. In that case the following script will get you started:

```zsh
export PATH="$PATH:/opt/homebrew/bin"
if which swiftlint > /dev/null; then
  swiftlint
else
  echo "warning: SwiftLint not installed, download from https://github.com/realm/SwiftLint"
fi
```



## Handling rule exceptions

Some times it is necessary to circumvent the exceptions given by SwiftLint and instead of breaking your head trying to shoehorn your code, you can use in-line comments to temporarily disable rules. You can find appropriate syntax to do this in [the SwiftLint documentation](https://realm.github.io/SwiftLint/#disable-rules-in-code).

For example you may want to allow for implicitly unwrapped optionals:
```swift
// swiftlint:disable:next implicitly_unwrapped_optional
var myVal: myInfo!
```

If there are lines that need to be skipped use the following:

```swift
// swiftlint:disable implicitly_unwrapped_optional
var myVal1: myInfo1!
var myVal2: myInfo2!
// swiftlint:enable implicitly_unwrapped_optional
```

Enjoy!



