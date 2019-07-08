---
title: INF HardwareId 指令
description: 发现新硬件向导和硬件更新向导的 Autorun.inf 文件的 [DeviceInstall] 部分中支持 INF HardwareId 指令。
ms.assetid: aceb4db2-ae00-47f3-994a-49541437e260
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
ms.openlocfilehash: b5a364030ddade721a392b3a7b3b513efcf03e59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346114"
---
# <a name="inf-hardwareid-directive"></a>INF HardwareId 指令


**请注意**   **HardwareId**中仅支持指令*Autorun.inf*文件。 此指令必须不能用于安装即插即用设备 INF 文件中。

 

从 Windows Vista 开始，发现新硬件向导和硬件更新向导支持 INF **HardwareId**中的指令 **\[DeviceInstall\]** 部分*Autorun.inf*文件。 一书的作者*Autorun.inf*可以使用这些**HardwareId**指令来指定为其启用了自动运行的应用程序提供的设备的即插即用 (PnP) 的 and Play 硬件标识符 (Id) 和安装驱动程序。

```ini
[DeviceInstall] 
 
HardwareId="pnp-hardware-id"
...
```

## <a name="entries"></a>条目


<a href="" id="-pnp-hardware-id-"></a>"*pnp-hardware-id*"  
此值指定一个即插即用设备硬件 id。 硬件 ID 必须括在双引号 （"）。

硬件 ID 可以是相当通用，例如 PCI\\VEN_1234 & DEV_1234，或非常具体，如 PCI\\VEN_1234 DEV_1234 SUBSYS_12345678 & REV_01。

对于每个硬件 Id 指令，可以指定只有一个即插即用硬件 ID。 若要指定多个硬件 Id，请使用多个硬件 Id 指令，每行一个。

<a name="remarks"></a>备注
-------

期间[硬件第一个安装](hardware-first-installation.md)，用户安装该设备的驱动程序之前安装硬件设备。 在这种情况下，发现新硬件向导会提示用户输入分发介质。

如果分发介质已自动启用*设备安装应用程序*，向导会分析*Autorun.inf*文件以查找**HardwareId**指令正在安装的设备相匹配的项。 如果向导找到**HardwareId**指令匹配的设备，该向导调用启用自动运行的应用程序，它将安装的驱动程序和特定于设备的应用程序，而该向导。

发现新硬件向导不会确定应用程序是否安装了设备的驱动程序。 在这种情况下，应用程序必须安装设备的驱动程序。 如果*Autorun.inf*文件不包括**HardwareId**安装时，该向导将设备标识的指令不会启动该应用程序和设备安装将继续。

虽然可能有多个**HardwareId**中的指令 **\[DeviceInstall\]** 一部分*Autorun.inf*文件中，每个指令应指定一个唯一的即插即用硬件 id。

 

 





