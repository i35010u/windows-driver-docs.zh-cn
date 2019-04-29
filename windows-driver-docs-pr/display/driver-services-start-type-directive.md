---
title: 驱动程序\服务启动类型指令
description: "\"Driver\\services\"启动类型指令是服务安装设置必需的所有显示器驱动程序。 Windows 显示器驱动程序模型 (WDDM) 驱动程序是插即用 (PnP)，因此必须按需启动，其中 StartType = 3。"
ms.assetid: 1B34DC18-EA81-44DB-B60A-D05B685E9321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e44b96055fcb0dad24a65f9db00f56182138be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358441"
---
# <a name="driverservices-start-type-directive"></a>驱动程序\\服务启动类型指令


*驱动程序\\services*开始 type 指令是服务安装设置必需的所有显示器驱动程序。 Windows 显示器驱动程序模型 (WDDM) 驱动程序是插即用 (PnP)，因此必须按需启动，其中*StartType* = 3。

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

 

 





