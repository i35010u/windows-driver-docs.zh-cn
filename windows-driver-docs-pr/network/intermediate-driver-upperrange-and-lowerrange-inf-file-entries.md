---
title: 中间驱动程序 UpperRange 和 LowerRange INF 文件项
description: 中间驱动程序 UpperRange 和 LowerRange INF 文件项
ms.assetid: 12a8561c-d410-45d0-8e96-898af6343f89
keywords:
- INF 文件 WDK 网络，中间驱动程序
- UpperRange INF 文件条目
- LowerRange INF 文件条目
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d9b4d6136adfda339cff0b4e1c4cb3910b37ce6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563609"
---
# <a name="intermediate-driver-upperrange-and-lowerrange-inf-file-entries"></a>中间驱动程序 UpperRange 和 LowerRange INF 文件项





本主题介绍如何使用**UpperRange**并**LowerRange** INF 文件条目来定义 NDIS 中间驱动程序绑定关系。

在网络驱动程序 INF 文件中， **UpperRange**项列出了可能的上限绑定并**LowerRange**项列出了可能较低的绑定。 有各种系统定义的值，这些列表。

有关筛选器中间驱动程序，必须设置的值**UpperRange**并**LowerRange**条目**noupper**并**nolower**，分别。 应仅在协议 INF 文件; 中定义这些项微型端口驱动程序 INF 文件中不需要它们。 下面的代码示例说明了这些项的筛选器的中间驱动程序。

```INF
HKR, Ndi\Interfaces, UpperRange, , noupper
HKR, Ndi\Interfaces, LowerRange, , nolower
```

在筛选器中间驱动程序， **FilterMediaTypes**协议 INF 文件中的条目定义的驱动程序绑定到其他驱动程序。 **FilterMediaTypes**指定由筛选器的中间驱动程序提供服务的媒体类型。 有关可能出现的媒体类型的列表，请参阅 Microsoft 提供的列表**LowerRange**中的值[指定绑定接口](specifying-binding-interfaces.md)。 下面的代码示例说明了此项的筛选器的中间驱动程序。

```INF
HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, tokenring, fddi, wan"
```

初始化筛选器的中间驱动程序时，它将自身插入到所有现有协议微型端口绑定，根据中列出的媒体类型**FilterMediaTypes**。

有关 MUX 中间驱动程序，还应始终设置**UpperRange**中的协议 INF 文件**noupper**。 设置**LowerRange**到一系列来自允许的这些值的值**LowerRange，** 中指定的那样[指定绑定接口](specifying-binding-interfaces.md)。 下面的代码示例说明了 MUX 中间驱动程序的下边缘这些条目。

```INF
HKR, Ndi\Interfaces, UpperRange, 0, "noupper"
HKR, Ndi\Interfaces, LowerRange, 0, "ndis5"
```

有关 MUX 中间驱动程序，还应始终设置**LowerRange**中的微型端口驱动程序 INF 文件**nolower**。 设置**UpperRange**到一系列来自允许的这些值的值**UpperRange，** 中指定的那样[指定绑定接口](specifying-binding-interfaces.md)。 下面的代码示例说明了 MUX 中间驱动程序虚拟微型端口这些条目。

```INF
HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
HKR, Ndi\Interfaces, LowerRange, 0, "nolower"
```

 

 





