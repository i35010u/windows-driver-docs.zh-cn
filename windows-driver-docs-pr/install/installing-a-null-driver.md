---
title: 安装 Null 驱动程序
description: 安装 Null 驱动程序
ms.assetid: 8684eade-3f25-48fe-94e7-a7e76d8072ad
keywords:
- 设备设置 WDK 设备安装，空驱动程序
- 设备安装 WDK，空驱动程序
- 安装设备 WDK，空驱动程序
- 空驱动程序 WDK 设备安装
- 不存在的驱动程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09e4a9526ad319682de6459925e9acea6b66557e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097285"
---
# <a name="installing-a-null-driver"></a>安装 Null 驱动程序





如果计算机上未使用设备且不应启动设备，则可能会安装 "null 驱动程序" (即设备的驱动程序) 不存在。 此类设备通常不存在于计算机上，但如果有，则可以安装 null 驱动程序。 此外，系统还会为没有函数驱动程序的设备安装 null 驱动程序。

若要在 INF 文件中指定 null 驱动程序，请使用如下所示的条目：

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

" *模型* " 部分中设备的硬件 ID 应专门使用子系统供应商 ID 和其他任何相关信息来标识设备。

操作系统将为设备创建 (*devnode*) 的设备节点，但如果设备无法在 raw 模式下执行，操作系统将不会启动设备，因为尚未向其分配功能驱动程序。 但请注意，如果设备有 [启动配置](../kernel/hardware-resources.md#logical-configuration-types-for-resource-lists)，将保留这些资源。

 

