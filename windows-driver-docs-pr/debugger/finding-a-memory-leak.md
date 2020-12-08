---
title: 查找内存泄漏
description: 查找内存泄漏
keywords:
- 内存泄漏
- 内存泄漏，调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4097e0803498485bcc4b79030aa15d55788c6cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838195"
---
# <a name="finding-a-memory-leak"></a>查找内存泄漏

如果进程从分页或非分页的池分配内存，但不释放内存，则会发生内存泄漏。 因此，这些有限的内存池会随着时间的推移而耗尽，导致 Windows 速度减慢。 如果内存完全耗尽，则可能会导致故障。

本节包括下列内容：

- 如果不确定系统中是否存在内存泄漏，[确定是否存在泄漏](determining-whether-a-leak-exists.md)说明了可以使用的方法。

- [查找内存泄漏 Kernel-Mode](finding-a-kernel-mode-memory-leak.md) 介绍了如何查找由内核模式驱动程序或组件导致的泄漏。

- [查找内存泄漏 User-Mode](finding-a-user-mode-memory-leak.md) 介绍了如何查找由用户模式驱动程序或应用程序引起的泄漏。

