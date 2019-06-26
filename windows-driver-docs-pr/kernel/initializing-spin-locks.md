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
ms.openlocfilehash: 5ad9eee4f77a68f0d5e8e466b149a7805113bbe2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369786"
---
# <a name="initializing-spin-locks"></a>初始化自旋锁





在调用之前需要对调用方提供 executive 旋转锁访问权限的任何支持例程，驱动程序必须调用[ **KeInitializeSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)初始化相应的 executive 自旋锁。 需要初始化 executive 自旋锁的支持例程包括：

- [**KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)以及随后[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)

- [**KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)以及随后[ **KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)

- [**KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))以及随后[ **KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)

- [**KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))以及随后[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)

- **ExInterlocked * Xxx*** 例程

然后再调用[ **IoConnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)并[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)，最低级别驱动程序必须调用[**KeInitializeSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)初始化为其提供了存储的中断自旋锁。

 

 




