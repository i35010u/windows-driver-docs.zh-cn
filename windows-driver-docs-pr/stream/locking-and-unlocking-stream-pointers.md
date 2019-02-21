---
title: 锁定和解锁 Stream 指针
description: 锁定和解锁 Stream 指针
ms.assetid: 3826a5bc-4ba5-4ada-a8aa-e7bbd949187e
keywords:
- 流指针 WDK AVStream，锁定和解锁
- 锁定的流指针 WDK AVStream
- 解锁的流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a978ee693c0b381155fae20bedbb61303dd9dc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526144"
---
# <a name="locking-and-unlocking-stream-pointers"></a>锁定和解锁 Stream 指针





每个流指针保持锁定状态： 已锁定或解锁。

锁定的流保证指针引用队列中的数据。 无法取消锁定的流指针指向的数据帧。 在这种情况下，微型驱动程序应尽量减少它们花费的时间保存锁定流指针。

不保证解锁的流指针引用队列中的数据帧。 通过解锁的流指针，微型驱动程序可以保留数据指针，但仍允许要取消的框架。

就可以访问由未锁定的流指针指向的数据。 如果*CancelCallback*中提供日常[ **KsStreamPointerClone** ](https://msdn.microsoft.com/library/windows/hardware/ff567129)调用[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)，您应该同步*CancelCallback*和它执行任何数据访问。 微型驱动程序必须确保它使用另一个线程时，取消回调例程并不删除流指针。

如果未调用取消回调例程**KsStreamPointerDelete**，可能不需要同步。

若要锁定流指针，调用[ **KsStreamPointerLock**](https://msdn.microsoft.com/library/windows/hardware/ff567134)。 若要解锁流指针，调用[ **KsStreamPointerUnlock**](https://msdn.microsoft.com/library/windows/hardware/ff567137)。

当取消 IRP 时，AVStream 的所有未锁定的流指针指向 IRP 中帧的调用取消回调。

仅当未使用时，请解锁前导和尾随边缘流指针。

 

 




