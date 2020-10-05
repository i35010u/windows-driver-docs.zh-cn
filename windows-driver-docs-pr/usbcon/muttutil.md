---
description: MuttUtil 在 MUTT 设备上执行各种任务。
title: MuttUtil
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f292793d905158eeb4032d7b14779cdb3e26a06
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733460"
---
# <a name="muttutil"></a>MuttUtil


MuttUtil 在 [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)上执行各种任务。

-   更新测试设备的固件。
-   安装适用于 MUTT 设备的驱动程序。
-   验证是否安装了设备且没有错误。
-   更改设备的操作总线速度。
-   将设备配置为在指定的时间段后发送恢复唤醒信号。
-   对于 MUTT Pack，它会将集线器设置为全速或高速操作;作为单 TT 或多 TT 中心。

MuttUtil 嵌入在所包含的测试脚本的安装部分，以确保将测试设备正确地升级到最新的固件。 该工具包含在 [MUTT](./index.md)软件包中。

## <a name="how-to-run-muttutil"></a>如何运行 MuttUtil


**MuttUtil 帮助**

运行以下命令以获取命令行选项的列表：

`MUTTUtil.exe`

**查找连接到系统的所有 MUTT 设备**

`MUTTUtil.exe -list`

``` syntax
       :   : HARDWARE ID                    : PROBLEM CODE : DRIVER
DEVICE : 0 : USB\VID_045E&PID_0611&REV_0034 : 0            : WINUSB
DEVICE : 1 : USB\VID_045E&PID_078E&REV_8011 : 28           :

Return value: 1
```

前面的命令指示系统具有 SuperMUTT (1) 和 (0) 附加的 MUTT Pack。 Winusb.sys，Microsoft 提供的内核模式驱动程序是 SuperMUTT 设备的函数驱动程序。 有关 Winusb.sys 的信息，请参阅 [WinUSB](winusb.md)。

MUTT Pack 设备的问题代码28表示没有为设备加载任何驱动程序。

**更改 MUTT 设备的个性**

MUTT 设备也用作 [USB UWP 应用示例](/samples/browse/)的测试设备。 对于这种情况，必须通过运行选项来更新固件 `-SetWinRTUsb` 。 在此练习中，SuperMUTT 设备设置为 WinRT 个性。

若要将其更改回 MUTT 个性，请使用此命令：

`MuttUtil.exe -# 1 -MuttPersonality`

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -MuttPersonality
Looking for MUTT devices
Send command to change device personality
Return value: 0

c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078F&REV_0034 :             0  : WINUSB
Return value: 1
```

请注意，硬件 ID 已更改为 USB \\ VID \_ 045E&PID \_ 078F&REV \_ 0037。 修订版本指示固件版本号。

**安装 MUTT 设备的驱动程序**

指定包含安装信息的驱动程序的 INF 文件。 例如，

`MUTTUtil.exe -UpdateDriver USBTCD.inf`

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver USBTCD.inf
Return value: 0

c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078F&REV_0034 :             0  : USBTCD
Return value: 1
```

上述命令将现有驱动程序替换为指定的 USBTCD.sys 驱动程序。 驱动程序包含在 [MUTT](./index.md)软件包中。

如果附加了多个 MUTT 设备，则可以同时更新驱动程序。

`MUTTUtil.exe -# 0 -# 1 -MultiUpdateDriver USBTCD.inf usbfx2.inf`

上述命令将为设备0安装 USBTCD.sys，为设备1安装 Winusb.sys，等等。

**在 MUTT 设备上更新固件**

`MuttUtil.exe -UpdateFirmware`

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateFirmware
Looking for MUTT devices
0: Updating device firmware from version 34 to version 37
  Erasing EEPROM -- this takes approx 30 seconds
Writing core firmware image
Writing Table at sector 0x09
Writing Table at sector 0x0A
Writing Table at sector 0x0B
Writing Table at sector 0x0C
Writing Table at sector 0x0D
Writing Table at sector 0x0E
Writing Table at sector 0x0F
Writing Table at sector 0x10
Writing Table at sector 0x08
0: Resetting device
Return value: 0
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078F&REV_0037 :             0  : USBTCD
Return value: 1
```

*仅当*设备中的版本为旧版本时，此命令才会通过固件更新 EEPROM。 固件映像嵌入在工具中。 如果设备的版本比该工具安装的固件新，则不会替换设备中的固件。 如果要替换设备中的固件而不考虑版本，请改为运行带有选项的 MuttUtil `-ForceUpdateFirmware` 。

更新固件的另一种方法是将其直接写入到 EEPROM 或 RAM。 为此，必须具有固件文件。

若要擦除 EEPROM，请使用 `-EraseEEPROM` 选项

**断开连接、重新连接和重新枚举设备**

`MuttUtil.exe -Reconnect`

`MuttUtil.exe -CyclePort`

前面的命令导致设备断开连接，然后重新连接到同一端口。

`-CyclePort`选项会使设备断开连接并连接回端口，但设备未通过电方式断开连接。 设备已断开连接并重新连接到软件。 此操作会导致重置设备，并且 PnP 管理器会重建设备节点。

若要重置 MUTT Pack 或 SuperMUTT Pack 设备的中心，请使用以下命令：

`MuttUtil.exe -# 1 -ResetHub`

**更改设备的速度**

可以使用以下命令更改 MUTT 设备的设备速度：

`MuttUtil.exe -# 0 -SetFullSpeed`

`MuttUtil.exe -# 1 -SetHighSpeed`

此命令会使设备断开连接，然后在指定速度的同一端口上重新连接。

如果要更改 MUTT Pack 或 SuperMUTT Pack 的中心速度以全速模式操作，请使用 `-HubFS` 命令：

`MuttUtil.exe -# 1 -HubFS`

**发送 resume 信号唤醒系统**

通常情况下，在执行某些用户操作时，设备 (以低功耗) 发送恢复信号。 可以使用以下命令模拟该行为：

`MuttUtil.exe -WakeAfterSuspend 5000`

命令将设备配置为在总线挂起5秒后发送恢复信号。

你还可以使用选项将设备配置为在总线挂起后的特定时间段内断开连接并重新连接 `-DisconnectAfterSuspend` 。

**在端口下游端口 MUTT Pack 和 SuperMUTT Pack 上设置和清除过流**

这些命令设置并清除 Mutt 的公开端口的过流 pin。

`MuttUtil.exe -# 1 -SetOvercurrent`

`MuttUtil.exe -# 1 -ClearOvercurrent`

**将集线器转换为 TT 高速中心-MUTT Pack 和 SuperMUTT Pack**

可以使用以下命令将集线器设置为多 TT 高速中心或单 TT 高速中心：

`MuttUtil.exe -# 1 -HubHSMultiTT`

`MuttUtil.exe -# 1 -HubHSSingleTT`

## <a name="related-topics"></a>相关主题
[USB 测试工具](usb-test-tools.md)  
[MUTT 软件包中的工具](mutt-software-package.md)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)