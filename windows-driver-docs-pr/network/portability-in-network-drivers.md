---
title: 网络驱动程序中的可移植性
description: 网络驱动程序中的可移植性
keywords:
- 网络驱动程序 WDK，移植驱动程序
- 可移植性 WDK 网络
- 移植驱动程序 WDK 网络
- NDIS 移植驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65eafd287936663727f279f1b06e6adb1ba04ca7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793421"
---
# <a name="portability-in-network-drivers"></a>网络驱动程序中的可移植性





应该编写 NDIS 驱动程序，以便在支持 Microsoft Windows 操作系统的所有平台上轻松地移植它们。 通常，从一个硬件平台移植到另一个硬件平台时，只需使用与系统兼容的编译器进行重新编译。

编写 NDIS 驱动程序时，请遵循以下准则：

-   避免调用特定于操作系统的函数。 相反，请使用 NDIS 等效函数。 NDIS 导出了一组丰富的支持函数来编写驱动程序，如果调用这些支持函数，则可以在支持 NDIS 的 Microsoft 操作系统之间移植代码。

-   以 C (专门指 ANSI C 标准) 编写驱动程序。 避免使用其他系统兼容编译器不支持的任何语言功能。 不要使用 ANSI C 标准指定为 "实现定义" 的任何功能。

-   避免依赖不同平台的大小和布局的数据类型。 例如，不要编写调用任何 C Run-Time 库函数的驱动程序代码，而不是调用 NDIS 提供的函数。

-   不要在内核模式下使用浮点运算。 如果尝试执行此类操作，则会出现严重错误。

-   使用 **\# ifdef** 和 **\# endif** 语句封装用于支持特定于平台的功能的代码。

 

 





