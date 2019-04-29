---
Description: MuttUtil MUTT 设备上执行各种任务。
title: MuttUtil
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ec748a8c01ba48162b56c6d0a98cd05468e4e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382710"
---
# <a name="muttutil"></a>MuttUtil


MuttUtil 上执行各种任务[MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。

-   更新测试设备的固件。
-   安装 MUTT 设备的驱动程序。
-   验证设备安装未出现错误。
-   更改设备的运行总线速度。
-   将设备配置为在指定的时间段后发送恢复唤醒信号。
-   对于 MUTT 包，它用于设置要以完整或高的速度; 运行的中心为单 TT 或多 TT 中心。

MuttUtil 嵌入中包括的测试脚本，以确保测试设备正确升级到最新的固件的安装部分。 该工具包含在[MUTT 软件包](https://go.microsoft.com/fwlink/p/?linkid=617710)。

## <a name="how-to-run-muttutil"></a>如何运行 MuttUtil


**MuttUtil 帮助**

运行以下命令来获取命令行选项的列表：

`MUTTUtil.exe`

**查找附加到系统的所有 MUTT 设备**

`MUTTUtil.exe -list`

``` syntax
       :   : HARDWARE ID                    : PROBLEM CODE : DRIVER
DEVICE : 0 : USB\VID_045E&PID_0611&REV_0034 : 0            : WINUSB
DEVICE : 1 : USB\VID_045E&PID_078E&REV_8011 : 28           :

Return value: 1
```

上述命令指示系统具有 SuperMUTT (1) 和附加 MUTT 包 (0)。 Microsoft 提供的内核模式驱动程序 Winusb.sys，是 SuperMUTT 设备功能驱动程序。 Winusb.sys 有关的信息，请参阅[WinUSB](winusb.md)。

MUTT 包设备有关的问题代码 28 指示没有驱动程序已加载的设备。

**更改 MUTT 设备的个人设置**

MUTT 设备也用作测试设备，以供[USB UWP 应用示例](https://go.microsoft.com/fwlink/p/?linkid=309716)。 对于这种情况下，必须通过运行更新固件`-SetWinRTUsb`选项。 在此练习中，SuperMUTT 设备设置为 WinRT 个性。

若要将其更改回 MUTT 个性，使用以下命令：

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

请注意，硬件 ID 将更改为 USB\\VID\_045E & PID\_078F & REV\_版本 0037。 修订版本指示固件版本数。

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

前一个命令通过指定 USBTCD.sys 驱动程序替换现有的驱动程序。 驱动程序包含在[MUTT 软件包](https://go.microsoft.com/fwlink/p/?linkid=617710)。

如果有多个 MUTT 设备连接时，会同时更新驱动程序。

`MUTTUtil.exe -# 0 -# 1 -MultiUpdateDriver USBTCD.inf usbfx2.inf`

上述命令会 USBTCD.sys 安装设备 0、 Winusb.sys 设备 1，依此类推。

**正在更新 MUTT 设备固件**

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

该命令使用固件更新 EEPROM*仅当*中设备的版本太旧。 在工具中嵌入的固件映像。 如果设备具有比固件工具安装较新版本，它不会替换中设备的固件。 如果你想要替换中不考虑版本设备的固件，运行与 MuttUtil`-ForceUpdateFirmware`选项。

更新固件的另一种方法是通过直接写入到的 EEPROM 或 RAM。 为此，您必须有固件文件。

若要清除 EEPROM，使用`-EraseEEPROM`选项

**断开连接、 重新连接后，并重新枚举设备**

`MuttUtil.exe -Reconnect`

`MuttUtil.exe -CyclePort`

上述命令会导致设备断开连接，然后在相同端口上然后重新连接。

`-CyclePort`选项将使设备断开连接并重新连接到该端口，但采用未断开连接设备。 设备已断开连接，并在软件中重新连接。 此操作会导致设备重置和 PnP 管理器重新生成设备节点。

若要重置 MUTT 包或 SuperMUTT 包设备的中心，请使用以下命令：

`MuttUtil.exe -# 1 -ResetHub`

**更改设备的速度**

可以使用此命令来更改 MUTT 设备的设备的速度：

`MuttUtil.exe -# 0 -SetFullSpeed`

`MuttUtil.exe -# 1 -SetHighSpeed`

该命令会导致设备断开连接，然后重新连接的指定速度在相同端口上。

如果你想要更改的中心，而 MUTT 包或 SuperMUTT 包的速度，若要在全速运行模式下操作使用`-HubFS`命令：

`MuttUtil.exe -# 1 -HubFS`

**发送唤醒系统的恢复信号**

通常情况下，恢复信号发送特定用户执行任何操作 （在低能耗） 设备。 可以使用以下命令来模拟此行为：

`MuttUtil.exe -WakeAfterSuspend 5000`

该命令用于配置设备发送恢复信号，5 秒后总线挂起。

此外可以配置设备断开连接并重新连接在一段时间后使用总线挂起`-DisconnectAfterSuspend`选项。

**设置和清除端口下游端口-MUTT 包和 SuperMUTT 包上的过电流**

这些命令设置和清除的 Mutt 包公开的端口的过流 pin。

`MuttUtil.exe -# 1 -SetOvercurrent`

`MuttUtil.exe -# 1 -ClearOvercurrent`

**将中心转换为 TT 高速集线器-MUTT 包和 SuperMUTT 包**

您可以设置要通过使用这些命令作为多 TT 高速集线器或单 TT 高速集线器进行操作的中心：

`MuttUtil.exe -# 1 -HubHSMultiTT`

`MuttUtil.exe -# 1 -HubHSSingleTT`

## <a name="related-topics"></a>相关主题
[USB 测试工具](usb-test-tools.md)  
[MUTT 软件包中的工具](mutt-software-package.md)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



