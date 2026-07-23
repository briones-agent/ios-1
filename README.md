# Cryptomator for iOS + React Native

This is an experimental fork of the official [Cryptomator for iOS](https://github.com/cryptomator/ios) with the sole purpose of testing brownfield support for Expo and React Native in large native-first codebases. Its commits serve as a reference for anyone interested in integrating React Native into an existing iOS app, especially those that don't want to refactor the whole project structure to accommodate React Native.

This project uses Expo's brownfield **isolated** approach, consuming a **prebuilt, shared Swift Package** rather than building React Native inside this repo — so the native app needs no Node, Yarn, or React Native toolchain.

## Integration steps

Check commits for detailed steps; full instructions are in the [expo-brownfield documentation](https://docs.expo.dev/brownfield/overview/).

1. **Prebuilt shared package**: React Native is built once (Expo SDK 57.0.0) and published as a binary Swift Package at [briones-agent/expo-brownfield-shared-ios](https://github.com/briones-agent/expo-brownfield-shared-ios).
2. **Add the package**: Xcode -> Add Package Dependencies -> that repo URL -> add the **`ExpoBrownfieldPackage`** product to the app target (deployment target >= 16.4).
3. **Add a React Native view**: `import ExpoBrownfieldKit`; `ReactNativeHostManager.shared.initialize()` at launch, then present `ReactNativeViewController(moduleName: "main")`. See `Cryptomator/ExpoIntegration.swift`.

<details>
<summary>Cryptomator for iOS</summary>

# Cryptomator for iOS

[![Build](https://github.com/cryptomator/ios/actions/workflows/build.yml/badge.svg)](https://github.com/cryptomator/ios/actions/workflows/build.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=cryptomator_ios&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=cryptomator_ios)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=cryptomator_ios&metric=coverage)](https://sonarcloud.io/summary/new_code?id=cryptomator_ios)
[![Mastodon](https://img.shields.io/mastodon/follow/176112?domain=mastodon.online&style=flat)](https://mastodon.online/@cryptomator)
[![Crowdin](https://badges.crowdin.net/cryptomator/localized.svg)](https://translate.cryptomator.org/)
[![Community](https://img.shields.io/badge/help-Community-orange.svg)](https://community.cryptomator.org)

Cryptomator offers multi-platform transparent client-side encryption of your files in the cloud.

Download on the App Store: https://apps.apple.com/app/cryptomator/id1560822163

## Special Shoutout

Continuous integration hosting is provided by [MacStadium](https://www.macstadium.com/company/opensource).

<a href="https://www.macstadium.com/company/opensource"><img src="https://uploads-ssl.webflow.com/5ac3c046c82724970fc60918/5c019d917bba312af7553b49_MacStadium-developerlogo.png" alt="MacStadium" height="100"></a>

## Building

### Create Secrets

If you are building with Xcode, create a `.cloud-access-secrets.sh` file in the `fastlane/scripts` directory. Its contents should look something like this:

```sh
#!/bin/sh
export BOX_CLIENT_ID=...
export BOX_CLIENT_SECRET=...
export DROPBOX_APP_KEY=...
export GOOGLE_DRIVE_CLIENT_ID=...
export GOOGLE_DRIVE_REDIRECT_URL_SCHEME=...
export MICROSOFT_GRAPH_CLIENT_ID=...
export MICROSOFT_GRAPH_REDIRECT_URI_SCHEME=...
export PCLOUD_APP_KEY=...
```

And then run `./scripts/create-cloud-access-secrets.sh` from the `fastlane` directory once. Of course, if you change the secrets, you have to run that script again.

If you are building via a CI system, set these secret environment variables accordingly.

## Contributing

Please read our [contribution guide](.github/CONTRIBUTING.md), if you would like to report a bug, ask a question or help us with coding.

This project uses [SwiftFormat](https://github.com/nicklockwood/SwiftFormat) and [SwiftLint](https://github.com/realm/SwiftLint) to enforce code style and conventions. Install these tools if you haven't already.

Please make sure that your code is correctly formatted and passes linter validations. The easiest way to do that is to set up a pre-commit hook. Create a file at `.git/hooks/pre-commit` with this content:

```sh
./Scripts/process.sh --staged
exit $?
```

And make your pre-commit hook executable:

```sh
chmod +x .git/hooks/pre-commit
```

## Code of Conduct

Help us keep Cryptomator open and inclusive. Please read and follow our [Code of Conduct](.github/CODE_OF_CONDUCT.md).

## License

Distributed under the GPLv3. See the LICENSE file for more info.

</details>
