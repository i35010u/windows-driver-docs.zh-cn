---
title: 查找内存泄漏
description: 查找内存泄漏
ms.assetid: 1227c5e8-d83b-4f27-aa69-6e54aebc3ad8
keywords:
- 内存泄漏
- 内存泄漏，调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5730b74408fa4c8c7c25b06f3f5deaf62ddc3641
ms.sourcegitcommit: a39a3f4c9f26968e00317574c0d8530ee8ab6f8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894235"
---
# <a name="finding-a-memory-leak"></a>查找内存泄漏

进程会将内存分配的分页或非分页池，但不会释放内存时，将发生内存泄漏。 因此，这些有限的内存池都用完随着时间推移，从而导致 Windows 速度下降。 如果完全耗尽内存，则可能会导致失败。

本部分包含下列内容：

- [确定是否存在泄漏](determining-whether-a-leak-exists.md)介绍一种技术，如果您不能确定，可以使用你的系统上是否存在内存泄漏。

- [查找内核模式内存泄漏](finding-a-kernel-mode-memory-leak.md)介绍了如何查找由内核模式驱动程序或组件导致的泄漏。

- [查找用户模式内存泄漏](finding-a-user-mode-memory-leak.md)介绍了如何查找用户模式驱动程序或应用程序导致的泄漏。

