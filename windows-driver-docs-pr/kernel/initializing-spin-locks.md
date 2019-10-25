---
title: 初始化自旋锁
description: 初始化自旋锁
ms.assetid: 7ed27e43-4406-4e64-b2c9-42b8a883efdb
keywords:
- 初始化自旋锁
- 旋转锁定 WDK 内核
- KeInitializeSpinLock
- executive 旋转锁定 WDK 内核
- 中断自旋锁定 WDK 内核
- 排队自旋锁 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 189beb3afabc77525658d99a913c1154ec159d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828289"
---
# <a name="initializing-spin-locks"></a>初始化自旋锁





在调用任何需要访问调用方提供的执行程序提供程序的支持例程之前，驱动程序必须调用[**KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)来初始化相应的执行程序旋转锁。 支持需要初始化的执行请求旋转锁定的例程包括：

- [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)和， [ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)

- [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)和， [ **KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)

- [**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))和， [ **KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)

- [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))和， [ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)

- **ExInterlocked * Xxx*** 例程

在调用[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)和[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)之前，最低级别的驱动程序必须调用[**KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)才能初始化它为其提供存储的中断自旋锁。

 

 




