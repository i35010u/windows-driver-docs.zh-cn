---
title: 重置 AVStream 编解码器中的状态
description: 重置 AVStream 编解码器中的状态
ms.assetid: c50014fe-bff0-43f4-8552-24e8e97f636b
keywords:
- AVStream 硬件编解码器支持 WDK，重置状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b0b45262f8b597ceaace2d65f738432da8b4f0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186329"
---
# <a name="resetting-state-in-avstream-codecs"></a>重置 AVStream 编解码器中的状态


为了丢弃流数据并重置流式传输状态，媒体流式处理管道会将 MFT \_ 消息 \_ 命令 \_ 刷新发送到 mft。 当 HW MFT 收到 MFT \_ 消息 \_ 命令刷新时 \_ ，MFT 会将值为 KSRESET 的 [**IOCTL \_ KS \_ 重置 \_ 状态**](/windows-hardware/drivers/ddi/ks/ni-ks-ioctl_ks_reset_state) 发送 \_ 到输入插针和输出插针。 微型驱动程序应订阅接收重置通知，方法是在[**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)的**Reset**成员中指定[*AVStrMiniPinReset*](/previous-versions/ff556354(v=vs.85))回调。

当驱动程序收到此 IOCTL 时，它应删除所有未完成的克隆指针并重置所有以前的内部状态。 驱动程序刷新挂起的 IO 请求后，将收到另一个 \_ 值为 KSRESET END 的 IOCTL KS \_ RESET \_ 状态 \_ 。

此时，微型驱动程序应该已准备好接受来自下一个流的新输入。

请注意，要使重置正常工作，微型驱动程序必须通过在[**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的**Connections**成员中提供[**KSTOPOLOGY \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)类型的数组，指定输入和输出插针之间的拓扑连接。

在以下情况下，也会发送 reset IOCTL。 当驱动程序在 \_ 流标题上设置 KSSTREAM 标头 \_ OPTIONSF \_ ENDOFSTREAM 标记并解除流指针的锁定时，KS 将刷新队列，这将生成一个 \_ \_ 值为 KSRESET 的 IOCTL KS 重置 \_ 状态调用 \_ 。

在这种情况下，当驱动程序收到没有前面的 begin 请求的结束请求时，驱动程序应设置 [**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)。**ResetState** 到 KSRESET \_ 结束。 这种情况仅适用于输出插针。

 

