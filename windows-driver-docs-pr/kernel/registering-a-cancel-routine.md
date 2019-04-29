---
title: 注册 Cancel 例程
description: 注册 Cancel 例程
ms.assetid: ebc63fb6-bf4d-4de3-9232-08d810c2f730
keywords:
- 正在取消 Irp，注册取消例程
- 取消例程注册
- 注册取消例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b5316b713470832d64a5454e9c7f68309ed177
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382653"
---
# <a name="registering-a-cancel-routine"></a>注册 Cancel 例程





如果设备驱动程序有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，可以注册其调度例程[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程通过提供其地址为输入到[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)。

如果驱动程序不具有*StartIo*例程，其调度例程必须执行以下操作之前队列 IRP 中以便做进一步的处理其他驱动程序例程：

1.  调用[ **IoAcquireCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff548196)。

2.  调用[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)输入 IRP 和驱动程序提供的入口点*取消*例程。

3.  调用[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)。

有关取消自旋锁的信息，请参阅[使用系统的取消自旋锁](using-the-system-s-cancel-spin-lock.md)。

管理其自己的 Irp，而不是使用 I/O 管理器提供的设备队列，队列的驱动程序不需要调用时获取取消自旋锁**IoSetCancelRoutine**。 但是，这些驱动程序，应检查*取消*例程的指针的**IoSetCancelRoutine**返回以确定是否*取消*例程已启动。

 

 




