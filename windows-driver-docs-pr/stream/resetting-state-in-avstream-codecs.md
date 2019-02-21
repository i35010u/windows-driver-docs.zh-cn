---
title: 重置 AVStream 编解码器中的状态
description: 重置 AVStream 编解码器中的状态
ms.assetid: c50014fe-bff0-43f4-8552-24e8e97f636b
keywords:
- AVStream 硬件编解码器支持 WDK，重置状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffaf707a6a58810d8fe1ef435c3d8e0908d3bc34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521515"
---
# <a name="resetting-state-in-avstream-codecs"></a>重置 AVStream 编解码器中的状态


若要放弃的流数据和重置流的状态，媒体流式处理管道，将发送 MFT\_消息\_命令\_刷新到 MFT。 当 HW MFT 收到 MFT\_消息\_命令\_刷新，请在 MFT 发送[ **IOCTL\_KS\_重置\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff560832)值为 KSRESET\_开始对输入和输出插针。 微型驱动程序应订阅可以接收通过指定重置通知[ *AVStrMiniPinReset* ](https://msdn.microsoft.com/library/windows/hardware/ff556354)中的回调**重置**隶属[ **KSPIN\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff563535)。

当驱动程序收到此 IOCTL 时，它应删除所有未完成克隆指针和重置所有以前的内部状态。 该驱动程序已挂起的 IO 请求刷新后，它将接收另一个 IOCTL\_KS\_重置\_值状态的 KSRESET\_结束。

此时，微型驱动程序应该已准备好接受新输入的下一步的流。

请注意，对于重置正常工作，微型驱动程序必须指定通过提供类型的数组输入和输出插针之间的拓扑连接[ **KSTOPOLOGY\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff567148)中**连接**的成员[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)结构。

重置 IOCTL 也会在以下方案中发送。 当驱动程序设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM 流标头标志并解锁流指针，KS 刷新该队列，用于生成 IOCTL\_KS\_重置\_值为 KSRESET 状态调用\_一端插入驱动程序。

在这种情况下，当驱动程序收到结束请求没有前面开始请求，该驱动程序应设置[ **KSPIN**](https://msdn.microsoft.com/library/windows/hardware/ff563483)。**ResetState** KSRESET 到\_结束。 这种情况下仅适用于输出插针。

 

 




