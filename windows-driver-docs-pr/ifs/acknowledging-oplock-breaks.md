---
title: 确认 Oplock 突破
description: 确认 Oplock 突破
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3efb2b18856c9c0018ad893910eb21a5744e0114
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838475"
---
# <a name="acknowledging-oplock-breaks"></a>确认 Oplock 突破


## <span id="oplock_break_conditions"></span><span id="OPLOCK_BREAK_CONDITIONS"></span>


Oplock 的所有者可以返回不同类型的确认。 与 [grant 请求](granting-oplocks.md)类似，这些确认以文件系统控制代码的形式发送 (即 [FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)s) 。 它们是：

-   FSCTL \_ OPLOCK \_ 中断 \_ 确认
    -   此 FSCTL 指示 oplock 所有者已完成流同步，并接受操作中断的级别 (Level 2 或 None) 。
-   FSCTL \_ OPLOCK \_ 中断 \_ ACK \_ NO \_ 2
    -   此 FSCTL 指示 oplock 所有者已完成流同步，但不需要2级 oplock。 相反，oplock 应断开为 "无" (也就是说，oplock 将完全) 释放。
-   FSCTL \_ OPBATCH \_ ACK \_ CLOSE \_ 挂起
    -   对于第1级 oplock，此 FSCTL 指示 oplock 所有者已完成流同步，并放弃 (完全不受此确认) 导致的 oplock 不会产生2级 oplock。

    <!-- -->

    -   对于批处理或筛选器 oplock，此 FSCTL 指示 oplock 所有者要关闭被授权者的流句柄。 操作被阻止，正在等待 oplock 中断的确认，继续等待，直到 oplock 所有者的句柄结束。
-   FSCTL \_ 请求 \_ OPLOCK
    -   通过 \_ \_ \_ \_ 在传递为 DeviceIoControl 的 lpInBuffer 参数的请求 oplock 输入缓冲区结构的 **Flags** 成员中指定请求 OPLOCK 输入标志确认 \_ \_ \_ ，此 FSCTL 用于确认 Windows 7 oplock 的中断。 *lpInBuffer* [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 仅当在 \_ \_ \_ \_ \_ **Flags** \_ \_ \_ 作为 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)的 *lpOutBuffer* 参数传递的请求 oplock 输出缓冲区结构的 Flags 成员中设置请求 oplock 输出标志确认必需标志时，才需要确认。 同样， [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 和 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 可用于从内核模式确认 Windows 7 oplock。 有关详细信息，请参阅 [**FSCTL \_ 请求 \_ OPLOCK**](./fsctl-request-oplock.md)。

相关的 FSCTL 代码是 FSCTL \_ OPLOCK \_ 中断 \_ 通知。 如果调用方想要在给定流上的 oplock 中断完成时收到通知，则使用此代码。 此调用可能会阻止。 当 FSCTL \_ OPLOCK \_ 中断 \_ 通知调用返回状态成功时 \_ ，这表示以下内容之一：

-   未授予 oplock。

-   调用时没有正在进行的 oplock 中断。

-   现在已完成任何正在进行的 oplock 中断。

若要在不需要确认时发送确认，则为错误，确认 FSCTL IRP 失败，状态为 \_ " \_ OPLOCK \_ 协议无效"。

如果关闭请求 oplock 中断的文件的句柄，则会隐式确认中断。 对于共享冲突的 oplock 中断，oplock 持有者可以关闭文件句柄，该句柄可确认 oplock 中断，并防止文件的其他用户发生共享冲突。

