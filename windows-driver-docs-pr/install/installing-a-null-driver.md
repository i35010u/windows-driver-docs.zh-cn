---
title: 安装 Null 驱动程序
description: 安装 Null 驱动程序
ms.assetid: 8684eade-3f25-48fe-94e7-a7e76d8072ad
keywords:
- 设备安装程序 WDK 设备安装，为 null 的驱动程序
- 设备安装 WDK，null 驱动程序
- 安装设备 WDK，null 驱动程序
- null 驱动程序 WDK 设备安装
- 不存在驱动程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e4be192c2a4809e36ec37cdbda048c8bed6237
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362941"
---
# <a name="installing-a-null-driver"></a>安装 Null 驱动程序





你可能会安装"null 驱动程序"（即，不存在驱动程序） 的设备，如果设备不在计算机上使用并不会启动。 此类设备通常不存在的计算机上，但如果是这样，你可以安装为 null 的驱动程序。 此外，系统将安装 null 没有功能驱动程序的设备的驱动程序。

若要在 INF 文件中指定 null 的驱动程序，请使用如下所示的条目：

```cpp
:
[MyModels]
%MyDeviceDescription% = MyNullInstallSection, &BadDeviceHardwareID%
:

[MyNullInstallSection]
; The install section is typically empty, but can contain entries that
; copy files or modify the registry.

[MyNullInstallSection.Services]
AddService = ,2    ; no value for the service name
:
```

中的设备的硬件 ID*模型*部分应识别的设备具体而言，使用子系统供应商 ID 和其他任何信息都是相关。

操作系统将创建一个设备节点 (*devnode*) 设备，但如果设备不能够执行在 raw 模式，操作系统将不启动设备因为功能驱动程序尚未分配给它。 请注意，但是，如果该设备已[启动配置](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#logical-configuration-types-for-resource-lists)，将保留这些资源。

 

 





