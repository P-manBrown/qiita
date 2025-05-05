---
title: 【Mac】コマンドでシステム設定の特定のパネルを開く方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## システム設定を開く

ターミナルからシステム設定を開くには以下のコマンドを実行します。

```terminal
open -a "System Settings"
```

または

```terminal
open "/System/Applications/System Settings.app"
```

システム設定の「一般」パネルが開きます。

## 特定のパネルを開く

以下のようにすると特定のパネルを指定して開けます。

```terminal
open "/System/Library/PreferencePanes/パネル.prefPane"
```

「外観」パネルを開く場合は次のようになります。

```terminal
open "/System/Library/PreferencePanes/Appearance.prefPane"
```

指定できるパネルの一覧は`ls /System/Library/PreferencePanes/`で取得できます。

```terminal
$ ls /System/Library/PreferencePanes/
Accounts.prefPane/                 Mouse.prefPane/
Appearance.prefPane/               Network.prefPane/
AppleIDPrefPane.prefPane/          Notifications.prefPane/
Battery.prefPane/                  Passwords.prefPane/
Bluetooth.prefPane/                PrintAndFax.prefPane/
ClassKitPreferencePane.prefPane/   PrintAndScan.prefPane/
ClassroomSettings.prefPane/        Profiles.prefPane/
DateAndTime.prefPane/              ScreenTime.prefPane/
DesktopScreenEffectsPref.prefPane/ Security.prefPane/
DigiHubDiscs.prefPane/             SharingPref.prefPane/
Displays.prefPane/                 SoftwareUpdate.prefPane/
Dock.prefPane/                     Sound.prefPane/
EnergySaver.prefPane/              Speech.prefPane/
EnergySaverPref.prefPane/          Spotlight.prefPane/
Expose.prefPane/                   StartupDisk.prefPane/
Extensions.prefPane/               TimeMachine.prefPane/
FamilySharingPrefPane.prefPane/    TouchID.prefPane/
InternetAccounts.prefPane/         Trackpad.prefPane/
Keyboard.prefPane/                 UniversalAccessPref.prefPane/
Localization.prefPane/             Wallet.prefPane/

```
