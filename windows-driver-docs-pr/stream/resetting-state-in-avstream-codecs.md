---
title: 重置 AVStream 编解码器中的状态
description: 重置 AVStream 编解码器中的状态
ms.assetid: c50014fe-bff0-43f4-8552-24e8e97f636b
keywords:
- AVStream 硬件编解码器支持 WDK，重置状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 939ccc64cbbbd501d09df0e4d035cbe07060263f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844950"
---
# <a name="resetting-state-in-avstream-codecs"></a>重置 AVStream 编解码器中的状态


为了丢弃流数据并重置流式传输状态，媒体流式处理管道会将 MFT 发送\_消息\_命令\_刷新到 MFT。 当 HW MFT 接收到 MFT\_消息\_命令\_FLUSH 时，MFT 会将[**IOCTL\_KS\_重置\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ni-ks-ioctl_ks_reset_state)，并将值 KSRESET\_开始到输入和输出插针。 微型驱动程序应订阅接收重置通知，方法是在[**KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)的**reset**成员中指定[*AVStrMiniPinReset*](https://docs.microsoft.com/previous-versions/ff556354(v=vs.85))回调。

当驱动程序收到此 IOCTL 时，它应删除所有未完成的克隆指针并重置所有以前的内部状态。 驱动程序刷新挂起的 IO 请求后，将收到另一个 IOCTL\_KS\_RESET\_状态，值为 KSRESET\_END。

此时，微型驱动程序应该已准备好接受来自下一个流的新输入。

请注意，若要使重置正常工作，微型驱动程序必须通过在 KSFILTER 的**Connections**成员中提供 KSTOPOLOGY 类型的数组[ **\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)来指定输入插针和输出插针之间的拓扑连接[ **\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构。

在以下情况下，也会发送 reset IOCTL。 当驱动程序在流标题上设置 KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM 标志并取消对流指针的锁定时，KS 将刷新队列，这将生成一个 IOCTL\_KS\_使用值KSRESET\_结束驱动程序。

在这种情况下，当驱动程序收到没有前面的 begin 请求的结束请求时，驱动程序应设置[**KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)。**RESETSTATE** KSRESET\_结束。 这种情况仅适用于输出插针。

 

 




