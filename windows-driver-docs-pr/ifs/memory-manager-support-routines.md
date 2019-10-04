---
title: 内存管理器支持例程
description: 内存管理器支持例程
ms.assetid: 9cdcddd7-a086-415d-a7bd-5d149019b8b4
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 283a8f97a859aa3f3a73c2ab0a4b1631d0d5e9e3
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955809"
---
# <a name="memory-manager-support-routines"></a>内存管理器支持例程

下表列出了系统提供的内存管理支持例程的子集，这些例程可由内核模式文件系统和文件系统（微筛选器和旧）筛选器驱动程序使用。 设备驱动程序无法使用这些例程。

除了此处所述的例程，文件系统和文件系统筛选器驱动程序还可以调用内核模式驱动程序体系结构引用中描述的任何**Mm**_Xxx_例程，并在*ntifs*中声明。

**头文件：** *ntifs*

**Prefix：Mm @ no__t-0_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **MmCanFileBeTruncated** | 检查文件是否可以截断。 |
| **MmDoesFileHaveUserWritableReferences** | 返回文件对象的可写引用数。 |
| **MmFlushImageSection** | 刷新文件的图像部分。 |
| **MmForceSectionClosed** | 删除不再使用的文件的数据和图像部分。 |
| **MmGetMaximumFileSectionSize** | 返回当前版本的 Windows 的文件部分可能的最大大小。 |
| **MmIsRecursiveIoFault** | 确定在 i/o 操作期间当前是否发生了页错误。 |
| **MmPrefetchPages** | 以最佳方式从辅助存储读取页面组。 |
| **MmSetAddressRangeModified** | 将当前在指定范围内的系统缓存中的有效页面标记为已修改。 |
