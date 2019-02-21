---
title: 初始化自旋锁
description: 初始化自旋锁
ms.assetid: 7ed27e43-4406-4e64-b2c9-42b8a883efdb
keywords:
- 初始化自旋锁
- 数值调节钮锁 WDK 内核
- KeInitializeSpinLock
- executive 自旋锁 WDK 内核
- 中断自旋锁 WDK 内核
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13a8d9c1b1a861209ee36b5d80865fc93d81107e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541326"
---
# <a name="initializing-spin-locks"></a>初始化自旋锁





在调用之前需要对调用方提供 executive 旋转锁访问权限的任何支持例程，驱动程序必须调用[ **KeInitializeSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff552160)初始化相应的 executive 自旋锁。 需要初始化 executive 自旋锁的支持例程包括：

- [**KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)以及随后[ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)

- [**KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)以及随后[ **KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150)

- [**KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)以及随后[ **KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)

- [**KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551908)以及随后[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)

- **ExInterlocked * Xxx*** 例程

然后再调用[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)并[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)，最低级别驱动程序必须调用[**KeInitializeSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff552160)初始化为其提供了存储的中断自旋锁。

 

 




