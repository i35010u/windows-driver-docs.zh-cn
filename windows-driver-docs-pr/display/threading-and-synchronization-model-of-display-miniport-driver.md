---
title: 线程处理和同步显示微型端口驱动程序模型
description: 显示微型端口驱动程序的线程和同步模型
ms.assetid: 4e5cf498-a2d1-44d5-b7a3-427f48b5da50
keywords:
- 线程处理 WDK 显示，微型端口驱动程序
- 同步 WDK 显示，微型端口驱动程序
- 微型端口驱动程序 WDK 显示同步
- 微型端口驱动程序 WDK 显示，线程处理
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 53da24251f21d6fa574d496fd91558b85b0085cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361216"
---
# <a name="threading-and-synchronization-model-of-display-miniport-driver"></a>显示微型端口驱动程序的线程和同步模型

多个线程可以在同一时间出现内显示微型端口驱动程序。 也就是说，一般情况下，显示微型端口驱动程序是可重入。 但是，某些调用到显示微型端口驱动程序不应为可重入因为它们访问图形硬件或访问跨线程的全局数据结构。 尽管可重入性或 nonreentrancy 无法选择在每次调用级别，但 Windows 显示器驱动程序模型 (WDDM) 预先分配，每次调用，以下定义准确地说什么驱动程序应调用的同步级别：

-   [线程处理和同步第三个级别](threading-and-synchronization-third-level.md)

-   [线程处理和同步第二个级别](threading-and-synchronization-second-level.md)

-   [线程处理和同步的第一个级别](threading-and-synchronization-first-level.md)

-   [线程处理和同步零级别](threading-and-synchronization-zero-level.md)

-   [线程同步和 TDR](thread-synchronization-and-tdr.md)

 

 





