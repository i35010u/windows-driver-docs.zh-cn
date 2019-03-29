---
title: 指定筛选器驱动程序绑定关系
description: 指定筛选器驱动程序绑定关系
ms.assetid: 0f0b81f4-2ac1-456c-aef0-73f3bbb7ce0e
keywords:
- 绑定关系的筛选器驱动程序 WDK 网络
- NDIS 筛选器驱动程序 WDK，绑定关系
- 绑定关系 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c5bf6bad865d6bc039f032f1dba208f9da0c8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569221"
---
# <a name="specifying-filter-driver-binding-relationships"></a>指定筛选器驱动程序绑定关系





在网络驱动程序 INF 文件中， **UpperRange**项列出了可能的上限绑定并**LowerRange**项列出了可能较低的绑定。 这些项可以包含各种系统定义的值。

有关筛选器驱动程序，必须设置的值**UpperRange**并**LowerRange**条目**noupper**并**nolower**分别。 下面的示例说明了这些筛选器驱动程序的 INF 文件条目。

```INF
HKR, Ndi\Interfaces,UpperRange,,"noupper"
HKR, Ndi\Interfaces,LowerRange,,"nolower"
```

在筛选器驱动程序， **FilterMediaTypes**筛选器 INF 文件中的条目定义的驱动程序绑定到其他驱动程序。 **FilterMediaTypes**指定媒体类型的筛选器驱动程序服务。 有关可能出现的媒体类型的列表，请参阅 Microsoft 提供的列表**LowerRange**中的值[指定绑定接口](specifying-binding-interfaces.md)。 下面的示例阐释**FilterMediaTypes**筛选器驱动程序的条目。

```INF
HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
```

当计算机加载筛选器驱动程序时，该驱动程序插入到的所有现有的协议适配器绑定，具体取决于该媒体类型**FilterMediaTypes**列出。

 

 





