---
title: 流类注册表值
description: 流类注册表值
ms.assetid: a6800f53-4d55-4a28-839b-47f0cecc17bf
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，注册表
- 流式处理微型驱动程序 WDK Windows 2000 内核，注册表
- 微型驱动程序 WDK Windows 2000 内核流式处理，注册表
- 注册表 WDK 流式处理微型驱动程序
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: e137c8f7fe5db607c8310bd06ef0c3768badfa08
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850229"
---
# <a name="stream-class-registry-values"></a>流类注册表值

若要在 *Stream.sys*下安装微型驱动程序，供应商必须提供符合 inf 文件语法的设备特定 inf 文件，如 [inf 文件部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section) 和 [inf 文件指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addcomponent-directive)中所述。 在此文件中，在 stream 类下运行的微型驱动程序可以在设备特定的 [**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) 节中设置特殊的注册表值。 这些注册表项作为二进制指示器：将其设置为十六进制值01以启用该功能。

Stream 类微型驱动程序可以使用以下注册表值：

**PageOutWhenUnopened**
  
此注册表项指示设备驱动程序应在打开时分页。 如果在未打开时不能将设备取出，则会关闭整个驱动程序的此功能。

**PowerDownWhenUnopened**
  
此注册表项指示设备在打开时应关闭电源。

**DriverUsesSWEnumToLoad**
  
仅软件设备驱动程序应使用此注册表字符串通知 stream 类：设备驱动程序需要不同于硬件设备驱动程序的 *AddRef/DecRef* 处理。

以下标志在 Windows 9x 上受支持，但在基于 NT 的操作系统中已过时：

**DontSuspendIfStreamsAreRunning**
  
此注册表变量在 Windows 2000 和更高版本的基于 NT 的操作系统中已过时。  (在此版本中，DirectShow 会侦听 power query，并使所有流在收到低功耗查询时暂停。 ) 应用程序仍可以通过调用 **SetThreadExecutionState**来通知系统正在使用它。 此例程在 Microsoft Windows SDK 文档中进行了介绍。 或者，驱动程序可以使用 [**PoSetSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)。

**OkToHibernate**
  
此注册表字符串仅对 Windows 98 上运行的驱动程序有效。 它不在基于 NT 的操作系统中使用。

下面是从 *Usbintel* 文件中提取的文件，该文件演示如何设置这些注册表值。 此文件是 UsbIntel 示例的一部分，可在驱动程序开发工具包 (DDK) 和 windows 驱动程序工具包中 (WDK) ，windows XP 通过 Windows 7 (Build 7600) 。

```inf
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
