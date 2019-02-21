---
title: 设置静态参数
description: 设置静态参数
ms.assetid: 0a41d8b4-8dd8-4a6b-a9b9-d19d07acd083
keywords:
- 添加注册表部分 WDK 网络、 静态参数
- 静态参数 WDK 网络
- 参数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9777de3fc8ee33f813cb98c29a4ccca738e1dfd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532933"
---
# <a name="setting-static-parameters"></a>设置静态参数





INF 文件一次只能设置静态参数。 此参数不能通过用户界面中的属性页重新配置。

*添加注册表部分*将 static 参数添加为 REG\_SZ 值与组件的实例键下面的示例中所示：

```INF
[a1.staticparams.reg]
HKR,, MediaType, 0, "1"
HKR,, InternalId, 0, "232"
```

*添加注册表部分*可以将任何供应商定义的静态参数添加到组件的实例键。

 

 





