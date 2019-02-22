---
title: 设备处于睡眠状态时排队的 I/O 请求
description: 设备处于睡眠状态时排队的 I/O 请求
ms.assetid: 8cc0cea0-e5be-4705-ad4d-13a44d536469
keywords:
- I/O WDK 电源管理
- 排队的 I/O 请求
- 睡眠电源管理 WDK 内核
- 睡眠状态的设备 WDK 电源管理
- 队列的 Irp
- power Irp WDK 内核，队列 I/O 请求
- 工作状态返回 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e8235955f0cfe59c2fcba47f5bb5dc65f4ef289
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540549"
---
# <a name="queuing-io-requests-while-a-device-is-sleeping"></a>设备处于睡眠状态时排队的 I/O 请求





设备处于睡眠状态，而其驱动程序应队列任何定向到设备的 I/O 请求。 [ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)， [ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)，并[ **IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)支持例程提供队列 Irp 的一种方法供延迟处理。 有关示例，请参阅排队机制的即插即用驱动程序中所述[持有传入 Irp 时设备暂停](holding-incoming-irps-when-a-device-is-paused.md)。

仅当设备处于工作 (D0) 状态时，驱动程序可以访问其设备。 当设备处于睡眠状态; 时，驱动程序无法接触任何设备注册首先，设备必须返回到工作状态中。

 

 




