---
title: 驱动程序\服务启动类型指令
description: "\"Driver\\services\" 启动类型指令是所有显示驱动程序的服务安装设置要求。 Windows 显示驱动程序模型 (WDDM) 驱动程序即插即用 (PnP) ，因此必须先开始，其中 StartType = 3。"
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6ad51149bee47a6ea676dda813d650adb483598
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809131"
---
# <a name="driverservices-start-type-directive"></a>驱动程序 \\ 服务启动类型指令


*驱动程序 \\ 服务* 启动类型指令是所有显示驱动程序的服务安装设置要求。 Windows 显示驱动程序模型 (WDDM) 驱动程序即插即用 (PnP) ，因此必须先开始，其中 *StartType* = 3。

例如：

``` syntax
; Service Installation Section
;

[R200_Service_Inst]
ServiceType    = 1                  ; SERVICE_KERNEL_DRIVER
StartType      = 3                  ; SERVICE_DEMAND_START
ErrorControl   = 0                  ; SERVICE_ERROR_IGNORE
LoadOrderGroup = Video
ServiceBinary  = %12%\r200.sys
```

 

 





