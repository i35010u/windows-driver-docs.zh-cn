---
title: 更改的功能
description: 更改的功能
ms.assetid: c7799406-d046-4261-8af7-7abbac18fa70
keywords:
- 64 位 WDK 内核，移植到驱动程序
- 移植到 64 位 Windows 的驱动程序
- 64 位指针 WDK 内核
- 整数大小 WDK 64 位
- 数据类型 WDK 64 位
- 64 位 WDK 内核，会发生什么变化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d3749f842322988a33b50dbddfd2aab23b8629a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383655"
---
# <a name="whats-changed"></a>更改的功能





在 32 位 Windows 上的整数、 长时间，以及指针的数据类型是大小相同，32 位。 此数据类型大小的方便一致性已聪明 C 程序员，许多用户遇到的理所当然它的一件好事。

在 64 位 Windows，但是，一致性这一假设不再有效。 指针现在为 64 位的长度，但整数和长时间数据类型保持同样的大小，像以前一样，32 位。 这是因为，虽然需要 64 位指针来适应系统与多达 16 TB 的虚拟内存，最多的数据仍正好可以满足到 32 位整数。 对于大多数应用程序，将默认整数大小更改为 64 位只是空间的在浪费。

在 32 位 Windows 平台上，操作系统自动修复对齐错误的内核模式内存，并使其对应用程序不可见。 这是用于调用进程和子代的任何进程。 64 位 Windows 中尚未实现此功能，通常显著降低性能。 因此，如果您的 32 位驱动程序包含未对齐的 bug，您需要移植到 64 位 Windows 时修复它们。

 

 




