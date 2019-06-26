---
title: 流类注册表值
description: 流类注册表值
ms.assetid: a6800f53-4d55-4a28-839b-47f0cecc17bf
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核注册表
- 流式处理微型驱动程序 WDK Windows 2000 内核注册表
- 微型驱动程序 WDK Windows 2000 内核流式处理、 注册表
- 注册表 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f71193b94d7c91e83ebf8d5529959f18b11695
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377811"
---
# <a name="stream-class-registry-values"></a>流类注册表值





若要安装下的微型驱动程序*Stream.sys*，供应商必须提供符合的特定于设备的 INF 文件[泛型 INF 文件要求](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。 在此文件中，流类下运行的微型驱动程序可以设置中特定于设备的特殊的注册表值[ **AddReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)部分。 这些注册表项提供作为二进制指示符： 将其设置为十六进制值 01 以启用功能。

Stream 类微型驱动程序可以使用以下注册表值：

<a href="" id="pageoutwhenunopened"></a>**PageOutWhenUnopened**  
此注册表项均表示未打开时的设备驱动程序应出页。 如果设备不能出页，在未打开时，此功能处于关闭状态的整个驱动程序。

<a href="" id="powerdownwhenunopened"></a>**PowerDownWhenUnopened**  
此注册表项均表示设备未打开时关闭。

<a href="" id="driverusesswenumtoload"></a>**DriverUsesSWEnumToLoad**  
仅限软件的设备驱动程序应使用此注册表字符串以通知流类的设备驱动程序需要不同*AddRef/DecRef*比硬件设备驱动程序处理。

在 Windows 9 上支持以下标志 x，但在基于 NT 的操作系统中已过时：

<a href="" id="dontsuspendifstreamsarerunning"></a>**DontSuspendIfStreamsAreRunning**  
此注册表变量是在 Windows 2000 和更高版本的基于 NT 的操作系统中已过时。 （截至此版本中，DirectShow 侦听 power 查询，并且当它收到低功耗查询中的所有流都加入暂停。）应用程序仍可以通知正在使用它通过调用系统**SetThreadExecutionState**。 此例程是 Microsoft Windows SDK 文档中所述。 或者，可以使用驱动程序[ **PoSetSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-posetsystemstate)。

<a href="" id="oktohibernate"></a>**OkToHibernate**  
此注册表字符串值仅对于驱动程序运行于 Windows 98 上有效。 在基于 NT 的操作系统中不使用它。

下面是提取*Usbintel.inf*演示如何设置这些注册表值的文件。 此文件的 UsbIntel 示例中，现已推出的驱动程序开发工具包 (DDK) 和适用于 Windows XP 到 Windows 7 (生成 7600) 的 Windows Driver Kit (WDK)。

```INF
[Intel.USBDCam]
Include= ks.inf, kscaptur.inf
Needs= KS.Registration,KSCAPTUR.Registration
AddReg= Intel.USBDCam.AddReg
CopyFiles=Intel.USBDCam.Files.Ext
; WIA
SubClass=StillImage
DeviceType=3
DeviceSubType=0x1
Capabilities=0x00000031
DeviceData=Intel.USBDCam.DeviceData
ICMProfiles="sRGB Color Space Profile.icm"
[Intel.USBDCam.AddReg]
HKR,,DevLoader,,*ntkern
HKR,,NTMPDriver,,usbintel.sys
HKR,,PageOutWhenUnopened,3,01
; WIA
HKR,,HardwareConfig,1,1
HKR,,USDClass,,"{0527d1d0-88c2-11d2-82c7-00c04f8ec183}"
```

 

 




