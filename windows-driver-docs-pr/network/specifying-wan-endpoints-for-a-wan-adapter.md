---
title: 指定 WAN 适配器的 WAN 终结点
description: 指定 WAN 适配器的 WAN 终结点
keywords:
- 添加-注册表--WDK 网络，WAN 适配器终结点
- WAN 适配器终结点 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd59c5b13fac909531addb7b205f6ae036151b69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832105"
---
# <a name="specifying-wan-endpoints-for-a-wan-adapter"></a>指定 WAN 适配器的 WAN 终结点





WAN 适配器的 INF 文件必须将 **WanEndpoints** 值添加到适配器的实例键。 **WanEndpoints** 是一个 REG \_ DWORD 值，它指定 WAN 适配器支持的端点 (也称为通道、线路或持有者通道) 。 例如，*基本速率接口* (BRI) ISDN 适配器的 **WanEndpoints** 值为2，而 *主速率接口* 的 **WanEndpoints** 值 (PRI) ISDN 适配器通常是23。

**注意**   Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用 ISDN 驱动程序。

 

下面是一个 *添加注册表部分* 的示例，它为 BRI ISDN 适配器添加 **WanEndpoints** 值2：

```INF
[a1.reg]
HKR,, WanEndpoints, 0x00010001, 2
```

 

 





