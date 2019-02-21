---
title: 注册 WDM 下边缘的微型端口驱动程序函数
description: 注册 WDM 下边缘的微型端口驱动程序函数
ms.assetid: 68048d36-d57c-4ad9-a15e-92b1d7866d4a
keywords:
- NDIS WDM 微型端口驱动程序 WDK 网络，将函数注册
- NDIS WDM 微型端口驱动程序 WDK 网络入口点函数
- NDIS 微型端口驱动程序 WDK 网络入口点函数的下边缘
- WDM 低边缘 WDK 网络，入口点函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2096d9945108bdf0fd1b18516da51bd2972af0c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523232"
---
# <a name="registering-miniport-driver-functions-for-wdm-lower-edge"></a>注册 WDM 下边缘的微型端口驱动程序函数





WDM 下边缘的微型端口驱动程序必须调用[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数，在其**DriverEntry**例程来注册特定入口点使用 NDIS 库函数。 这些入口点函数编写微型端口驱动程序的上边缘和中所述[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。 但是，具有 WDM 下边缘的微型端口驱动程序不需要设置某些入口点函数。 例如，以下入口点函数未设置原因如下：

-   [*MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)， [ *MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)， [ *MiniportEnableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559380)，和[ *MiniportDisableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559375)

    微型端口驱动程序未收到来自物理网络接口卡 (NIC) 的中断，因为它不需要这些入口点例程。 适用于微型端口驱动程序在总线上的数据包到达时，为特定的总线驱动程序将接收中断。 然后，总线驱动程序会通知微型端口驱动程序。

-   [*MiniportSharedMemoryAllocateComplete*](https://msdn.microsoft.com/library/windows/hardware/ff559446)

    微型端口驱动程序不会分配共享的内存，因为未指定完成入口点例程。

-   [*MiniportCheckForHangEx*](https://msdn.microsoft.com/library/windows/hardware/ff559346)

    NDIS 以确定是否其微型端口实例停止响应，基于发送，以便此例程不通常需要请求时超时，可将微型端口驱动程序。

 

 





