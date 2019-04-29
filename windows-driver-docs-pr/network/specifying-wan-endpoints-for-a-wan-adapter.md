---
title: 指定 WAN 适配器的 WAN 终结点
description: 指定 WAN 适配器的 WAN 终结点
ms.assetid: e6dd12c3-03e3-4f7d-8ad7-2511bf46c4f8
keywords:
- 添加注册表部分 WDK 网络连接、 WAN 适配器终结点
- WAN 适配器终结点 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e22610913c44b8aff40210aa29ef42e3150a2322
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388117"
---
# <a name="specifying-wan-endpoints-for-a-wan-adapter"></a>指定 WAN 适配器的 WAN 终结点





WAN 适配器的 INF 文件必须添加**WanEndpoints**到适配器的实例键的值。 **WanEndpoints**是 REG\_DWORD 值，该值指定数量的终结点 （也称为通道、 线路或持有者渠道） 支持的 WAN 适配器。 例如， **WanEndpoints**值*基本速率接口*(BRI) ISDN 适配器是 2，而**WanEndpoints**值*主速率接口*(PRI) ISDN 适配器通常为 23。

**请注意**   ISDN 驱动程序在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

以下是一种*添加注册表部分*，它将**WanEndpoints**值为 2，BRI ISDN 适配器：

```INF
[a1.reg]
HKR,, WanEndpoints, 0x00010001, 2
```

 

 





