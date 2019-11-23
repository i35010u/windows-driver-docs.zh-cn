---
title: 内核支持例程
description: 内核支持例程
ms.assetid: aa4a1a16-06df-4795-ac26-5728e6f2df11
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2316874463bdd7e66397f2edbed1b2f0f6825de4
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955801"
---
# <a name="kernel-support-routines"></a>内核支持例程

下表列出了系统提供的可由内核模式文件系统和文件系统（微筛选器和旧版）筛选器驱动程序使用的系统提供的内核支持例程的子集，并保留了某些系统以供系统使用。 不能将以下例程用于设备驱动程序。

除了此处所述的例程，文件系统和文件系统筛选器驱动程序还可以调用内核模式驱动程序体系结构参考部分中所述的任何**Ke**_Xxx_例程，并在*ntifs*中声明。

**头文件：** *ntifs*

**前缀： Ke**_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **KeAcquireQueuedSpinLock** | 保留供系统使用。 |
| **KeAttachProcess** | 已过时。 改用**KeStackAttachProcess** 。 |
| **KeDetachProcess** | 已过时。 改用**KeUnstackAttachProcess** 。 |
| **KeInitializeMutant** | 保留供系统使用。 请参阅**KeInitializeMutex**。 |
| **KeInitializeQueue** | 初始化一个队列对象，线程可以在该对象上等待输入。 |
| **KeInsertHeadQueue** | 如果在给定队列的开头不能立即使用条目来满足线程等待，则插入该项。|
| **KeInsertQueue** | 如果某个条目无法立即使用条目来满足线程等待，则在给定队列的尾部插入该项。 |
| **KeReadStateMutant** | 保留供系统使用。 请参阅**KeReadStateMutex**。 |
| **KeReadStateQueue** | 保留供系统使用。 |
| **KeReleaseMutant** | 保留供系统使用。 请参阅**KeReleaseMutex**。 |
| **KeReleaseQueuedSpinLock** | 保留供系统使用。 |
| **KeRemoveQueue** | 向调用线程提供一个指向给定队列对象中的取消排队项的指针，或允许调用方在队列对象上等待，直到达到可选的超时间隔。 |
| **KeRundownQueue** | 清理队列对象，刷新任何排队的条目。 |
| **KeSetIdealProcessorThread** | 保留供系统使用。 |
| **KeStackAttachProcess** | 将当前线程附加到目标进程的地址空间。 |
| **KeTryToAcquireQueuedSpinLock** | 保留供系统使用。 |
| **KeUnstackDetachProcess** | 将当前线程与进程的地址空间分离，并还原以前的附加状态。 请特别小心使用此例程。 （请参见 "备注" 部分。） |
