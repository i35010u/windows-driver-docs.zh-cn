---
title: 筛选器安装
description: 筛选器安装
ms.assetid: 118d9fd9-c499-4371-9084-a4368a78f5e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40fedbe775c3c9534646ecc45c71d85f2ef19cf7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355881"
---
# <a name="filter-installation"></a>筛选器安装


崩溃转储筛选器驱动程序可以安装在崩溃转储堆栈中，通过添加以下代码示例中所示的注册表项中的服务名称。 初始化故障转储或休眠状态时，加载转储驱动程序。 在这一次加载的注册表项中所述的筛选器驱动程序。

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CrashControl

DumpFilters REG_MULTI_SZ DriverName

e.g. dumpfltr.sys
```

 

 




