---
title: Executive 支持例程
description: Executive 支持例程
ms.assetid: f86b942c-9a3f-495b-9623-fd0656ec4a7a
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: b652b6a837e587d2df429c8379e1060bfc64ae9d
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955795"
---
# <a name="executive-support-routines"></a>Executive 支持例程

以下系统提供的执行支持函数和宏可由内核模式文件系统和微筛选器和旧筛选器驱动程序（而不是设备驱动程序）调用。 有些函数保留供系统使用。

除了此处所述的例程，文件系统和筛选器驱动程序还可以调用在*ntifs*中声明的内核模式驱动程序体系结构参考部分中描述的任何**Ex**_Xxx_例程。

**头文件：** *ntifs*

**前缀： Ex * Xxx***

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **ExAdjustLookasideDepth** | 保留供系统使用。 |
| **ExDisableResourceBoost** | 保留供系统使用。 |
| **ExDisableResourceBoostLite** | 保留供系统使用。 |
| **ExInitializeWorkItem** | 使用调用方提供的上下文和回调例程初始化工作队列项，以便在系统工作线程得到控制时排队等待执行。 请特别小心使用此例程。|
| **ExQueryPoolBlockSize** | 已过时。 |
| **ExQueueWorkItem** | 将给定工作项插入到队列中，系统工作线程将从该队列中移除该项，并向调用方提供给 ExInitializeWorkItem 的例程提供控制。 请特别小心使用此例程。 |
