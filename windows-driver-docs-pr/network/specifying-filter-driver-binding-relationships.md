---
title: 指定筛选器驱动程序绑定关系
description: 指定筛选器驱动程序绑定关系
keywords:
- 筛选器驱动程序 WDK 网络，绑定关系
- NDIS 筛选器驱动程序 WDK，绑定关系
- 绑定关系 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b788c589e2aedb36f94eb3de847521fd55b921d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814919"
---
# <a name="specifying-filter-driver-binding-relationships"></a>指定筛选器驱动程序绑定关系





在网络驱动程序 INF 文件中， **UpperRange** 条目列出了可能的上限绑定， **LowerRange** 条目列出了可能的下限。 这些项可以包含各种系统定义的值。

对于筛选器驱动程序，必须分别将 **UpperRange** 和 **LowerRange** 条目的值设置为 **noupper** 和 **nolower**。 下面的示例演示了筛选器驱动程序的这些 INF 文件项。

```INF
HKR, Ndi\Interfaces,UpperRange,,"noupper"
HKR, Ndi\Interfaces,LowerRange,,"nolower"
```

在筛选器驱动程序中，筛选器 INF 文件中的 **FilterMediaTypes** 条目定义驱动程序与其他驱动程序的绑定。 **FilterMediaTypes** 指定筛选器驱动程序服务的媒体类型。 有关可能的媒体类型的列表，请参阅 [指定绑定接口](specifying-binding-interfaces.md)中 Microsoft 提供的 **LowerRange** 值的列表。 下面的示例演示了筛选器驱动程序的 **FilterMediaTypes** 项。

```INF
HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
```

当计算机加载筛选器驱动程序时，驱动程序将插入到所有现有的协议到适配器绑定中，具体取决于 **FilterMediaTypes** 列出的媒体类型。

 

 





