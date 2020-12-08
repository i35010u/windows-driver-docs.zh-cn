---
title: 设置启动类型值
description: 设置启动类型值
keywords:
- INF 文件，WDK 显示，开始类型值
- 开始类型值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2d10877cc984a0d44d5d244c0e251fdc09c7ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822449"
---
# <a name="setting-the-start-type-value"></a>设置启动类型值


应将写入的显示驱动程序设置为 Windows 显示驱动程序模型 (WDDM) ，以便在 Windows Vista 和更高版本上（而不是在运行 Windows Vista 之前的操作系统上运行的显示驱动程序）开始按需运行。 此更改的原因在于，在 Windows Vista 之前的操作系统中不存在基于清单和映像的安装功能。 应将 **StartType** 条目的值设置为 "服务 \_ 需求 \_ 开始 (3) 而不是" 服务 \_ 系统 \_ 启动 (1) 。

下面的示例演示了一个服务安装部分，其中包含 " **StartType** " 项设置为 "服务需求开始" 的值， \_ \_ 以指示按需启动显示微型端口驱动程序：

```inf
;
; Service Installation Section
;

[R200_Service_Inst]
ServiceType    = 1        ; SERVICE_KERNEL_DRIVER
StartType      = 3        ; SERVICE_DEMAND_START
ErrorControl   = 0        ; SERVICE_ERROR_IGNORE
LoadOrderGroup = Video
ServiceBinary  = %12%\r200.sys
```

有关与 **AddService** 指令关联的服务安装节的详细信息，请参阅 [**INF AddService 指令**](../install/inf-addservice-directive.md)。

 

