---
title: INF HardwareId 指令
description: "\"发现新硬件向导\" 和 \"硬件更新向导\" 支持自动运行 .inf 文件的 [DeviceInstall] 部分中的 INF HardwareId 指令。"
keywords:
- INF HardwareId 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF HardwareId Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6262d77ca3d0e4e7778cc079da76365d9b3e484
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840051"
---
# <a name="inf-hardwareid-directive"></a>INF HardwareId 指令


**注意** 仅 *自动运行的 .inf* 文件中支持 **HardwareId** 指令。 此指令不得用于用于 PnP 设备安装的 INF 文件中。

 

从 Windows Vista 开始，"发现新硬件向导" 和 "硬件更新向导" 支持 *自动运行 .inf* 文件的 **\[ DEVICEINSTALL \]** 部分中的 INF **HardwareId** 指令。 *自动运行 .inf* 的作者可以使用这些 **HardwareId** 指令指定) 硬件标识符即插即用 (PnP 硬件标识符 (Id) 启用了自动启用的应用程序提供并安装驱动程序的设备。

```inf
[DeviceInstall] 
 
HardwareId="pnp-hardware-id"
...
```

## <a name="entries"></a>项


<a href="" id="-pnp-hardware-id-"></a>"*pnp-硬件 id*"  
此值指定 PnP 设备硬件 ID。 硬件 ID 必须用双引号引起来， ( ") 。

硬件 ID 可能是相当通用的，如 PCI \\ VEN_1234&DEV_1234 或非常具体，如 pci VEN_1234&DEV_1234&SUBSYS_12345678&REV_01 \\ 。

每个 HardwareId 指令只能指定一个 PnP 硬件 ID。 若要指定多个硬件 Id，请使用多个 HardwareId 指令（每行一个）。

<a name="remarks"></a>备注
-------

在进行 [硬件首次安装](hardware-first-installation.md)期间，用户在安装该设备的驱动程序之前安装硬件设备。 在这种情况下，"发现新硬件" 向导会提示用户提供分发介质。

如果分发介质具有启用了自动运行的 *设备安装应用程序*，则向导会分析 *自动运行的 .inf* 文件，以查找与正在安装的设备匹配的 **HardwareId** 指令条目。 如果向导找到与设备匹配的 **HardwareId** 指令，则向导将调用启用了自动激活的应用程序，该应用程序将安装驱动程序和设备特定的应用程序，而不是向导。

"发现新硬件" 向导不确定应用程序是否安装了设备驱动程序。 在这种情况下，应用程序必须安装设备驱动程序。 如果可 *执行文件不* 包含标识正在安装的设备的 **HardwareId** 指令，则向导将不会启动该应用程序并继续安装设备。

尽管 *自动运行 .inf* 文件的 **\[ DeviceInstall \]** 部分中可能有多个 **HardwareId** 指令，但每个指令应指定唯一的 PnP 硬件 ID。

 

 





