---
title: 中间驱动程序 UpperRange 和 LowerRange INF 文件项
description: 中间驱动程序 UpperRange 和 LowerRange INF 文件项
keywords:
- INF 文件 WDK 网络，中间驱动程序
- UpperRange INF 文件条目
- LowerRange INF 文件条目
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea751b621bfcef32227fb48073ce61c948e309dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818377"
---
# <a name="intermediate-driver-upperrange-and-lowerrange-inf-file-entries"></a>中间驱动程序 UpperRange 和 LowerRange INF 文件项





本主题说明如何使用 **UpperRange** 和 **LowerRange** INF 文件项来定义 NDIS 中间驱动程序绑定关系。

在网络驱动程序 INF 文件中， **UpperRange** 条目列出了可能的上限绑定， **LowerRange** 条目列出了可能的下限。 这些列表有各种系统定义的值。

对于筛选器中间驱动程序，必须分别将 **UpperRange** 和 **LowerRange** 条目的值设置为 **noupper** 和 **nolower**。 只应在协议 INF 文件中定义这些项;它们在微型端口驱动程序 INF 文件中不是必需的。 下面的代码示例演示了筛选器中间驱动程序的这些条目。

```INF
HKR, Ndi\Interfaces, UpperRange, , noupper
HKR, Ndi\Interfaces, LowerRange, , nolower
```

在筛选器中间驱动程序中，协议 INF 文件中的 **FilterMediaTypes** 条目定义驱动程序与其他驱动程序的绑定。 **FilterMediaTypes** 指定由筛选器中间驱动程序提供服务的媒体类型。 有关可能的媒体类型的列表，请参阅 [指定绑定接口](specifying-binding-interfaces.md)中 Microsoft 提供的 **LowerRange** 值的列表。 下面的代码示例演示了筛选器中间驱动程序的此项。

```INF
HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, tokenring, fddi, wan"
```

当初始化筛选器中间驱动程序时，它会根据 **FilterMediaTypes** 中列出的媒体类型，将自身插入到所有现有的协议到微型端口的绑定中。

对于 MUX 中间驱动程序，应始终将协议 INF 文件中的 **UpperRange** 设置为 **noupper**。 将 **LowerRange** 设置为从允许用于 LowerRange 的值中获取的值列表（在指定 [绑定接口](specifying-binding-interfaces.md)中指定 **）** 。 下面的代码示例演示了 MUX 中间驱动程序的下边缘的这些项。

```INF
HKR, Ndi\Interfaces, UpperRange, 0, "noupper"
HKR, Ndi\Interfaces, LowerRange, 0, "ndis5"
```

对于 MUX 中间驱动程序，应始终将微型端口驱动程序 INF 文件中的 **LowerRange** 设置为 **nolower**。 将 **UpperRange** 设置为从 **UpperRange** 允许的值中获取的值列表，如 [指定绑定接口](specifying-binding-interfaces.md)中所指定。 下面的代码示例演示了 MUX 中间驱动程序虚拟小型端口的这些项。

```INF
HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
HKR, Ndi\Interfaces, LowerRange, 0, "nolower"
```

 

 





