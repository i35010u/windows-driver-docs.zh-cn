---
title: 网络驱动程序中的可移植性
description: 网络驱动程序中的可移植性
ms.assetid: 2cc74131-a80b-4d21-b969-56b61d1f7269
keywords:
- 网络驱动程序 WDK，将驱动程序移植
- 可移植性 WDK 网络
- 移植驱动程序 WDK 网络
- NDIS 移植驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 918a55747ae4a99eba93018c24f379a1fbe6963d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524011"
---
# <a name="portability-in-network-drivers"></a>网络驱动程序中的可移植性





应编写的 NDIS 驱动程序，以便可轻松地移植跨所有 Microsoft Windows 操作系统的支持的平台。 一般情况下，从不同的硬件平台移植到另一个应只需要与系统兼容的编译器重新编译。

当您编写的 NDIS 驱动程序时，请遵循以下准则：

-   请避免调用特定于操作系统的函数。 相反，使用 NDIS 等效的函数。 NDIS 导出一组丰富的支持函数编写驱动程序，且如果您在调用这些支持函数，你可以支持 NDIS 的 Microsoft 操作系统之间代码移植。

-   在 C 中 （具体而言，ANSI C 标准） 编写驱动程序。 避免使用任何其他系统兼容编译器不支持的语言功能。 不使用任何功能的 ANSI C 标准将指定为"定义的实现。"

-   避免依赖于数据类型的大小和布局平台而异。 例如，不编写调用而不是提供 NDIS 函数的任何 C 运行时库函数的驱动程序代码。

-   不要在内核模式下使用浮点运算。 如果在尝试执行此类操作，将发生致命错误。

-   使用 **\#ifdef**并 **\#endif**语句来封装用于支持特定于平台的功能的代码。

 

 





