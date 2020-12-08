---
title: 筛选器安装
description: 筛选器安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a95e8a841ba1a6bf66f82830385aa119ad4d92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804611"
---
# <a name="filter-installation"></a>筛选器安装


故障转储筛选器驱动程序可以安装在故障转储堆栈中，方法是在下面的代码示例中所示的注册表项中添加服务名称。 当初始化故障转储或休眠时，将加载转储驱动程序。 此时会加载注册表项中提到的筛选器驱动程序。

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CrashControl

DumpFilters REG_MULTI_SZ DriverName

e.g. dumpfltr.sys
```

 

 




