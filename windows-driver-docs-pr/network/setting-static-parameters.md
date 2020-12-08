---
title: 设置静态参数
description: 设置静态参数
keywords:
- 添加-注册表-每节 WDK 网络，静态参数
- 静态参数 WDK 网络
- 参数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a19806af68a6c38a4626ea114b53519172a4ece
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801303"
---
# <a name="setting-static-parameters"></a>设置静态参数





INF 文件仅设置一次静态参数。 不能通过用户界面中的 "属性" 页重新配置此参数。

*添加注册表部分* 将静态参数作为 REG \_ SZ 值添加到组件的实例键，如以下示例中所示：

```INF
[a1.staticparams.reg]
HKR,, MediaType, 0, "1"
HKR,, InternalId, 0, "232"
```

" *添加注册表" 部分* 可将任何供应商定义的静态参数添加到组件的实例键。

 

 





