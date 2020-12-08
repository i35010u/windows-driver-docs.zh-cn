---
title: 更改的功能
description: 更改的功能
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
- 64位指针 WDK 内核
- integer size WDK 64 位
- 数据类型 WDK 64 位
- 64位 WDK 内核，已更改
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e097d67efb4180b5749a1bb1027e5396515d8b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829999"
---
# <a name="whats-changed"></a>更改的功能





在32位 Windows 上，integer、long 和指针数据类型都具有相同的大小-32 位。 数据类型大小的这种简便的一致性是 boon 的，很多人都在使用它。

但在64位 Windows 上，这种一致性假设不再有效。 指针的长度现在为64位，但整型和 long 数据类型的大小与以前的大小相同（32位）。 这是因为，尽管需要64位指针才能容纳大小为 16 TB 的虚拟内存的系统，但大多数数据仍适合于32位整数。 对于大多数应用程序，将默认整数大小更改为64位只是浪费空间。

在32位 Windows 平台上，操作系统会自动修复内核模式内存对齐错误，并使其对应用程序不可见。 它针对调用进程和任何子代进程执行此操作。 此功能通常会显著降低性能，而不是在64位 Windows 中实现的。 因此，如果你的32位驱动程序包含不一致的 bug，则在迁移到64位 Windows 时，你将需要修复这些 bug。

 

 




