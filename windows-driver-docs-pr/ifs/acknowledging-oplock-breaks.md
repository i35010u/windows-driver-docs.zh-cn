---
title: 确认 Oplock 突破
description: 确认 Oplock 突破
ms.assetid: ea5bcd1e-d22c-4f80-89e4-1a61e43959dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990be83f5b82e089aabc7304df4ff82cacee51d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841497"
---
# <a name="acknowledging-oplock-breaks"></a>确认 Oplock 突破


## <span id="oplock_break_conditions"></span><span id="OPLOCK_BREAK_CONDITIONS"></span>


Oplock 的所有者可以返回不同类型的确认。 与[grant 请求](granting-oplocks.md)类似，这些确认作为文件系统控制代码（即[FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)）发送。 它们是：

-   FSCTL\_OPLOCK\_中断\_确认
    -   此 FSCTL 指示 oplock 所有者已完成流同步，并接受 oplock 中断的级别（级别2或无）。
-   FSCTL\_OPLOCK\_中断\_ACK\_NO\_2
    -   此 FSCTL 指示 oplock 所有者已完成流同步，但不需要2级 oplock。 相反，oplock 应断开为 "无" （即，oplock 要完全释放）。
-   FSCTL\_OPBATCH\_ACK\_关闭\_挂起
    -   对于第1级 oplock，此 FSCTL 表示 oplock 所有者已完成流同步，并已完全放弃 oplock （此确认不会导致第2级 oplock）。

    <!-- -->

    -   对于批处理或筛选器 oplock，此 FSCTL 指示 oplock 所有者要关闭被授权者的流句柄。 操作被阻止，正在等待 oplock 中断的确认，继续等待，直到 oplock 所有者的句柄结束。
-   FSCTL\_请求\_OPLOCK
    -   通过在请求的**Flags**成员中指定请求\_OPLOCK\_输入\_标志\_确认\_OPLOCK\_输入\_传递为[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)的*lpInBuffer*参数的缓冲结构，则此 FSCTL 用于确认 Windows 7 oplock 的中断。 仅当请求\_OPLOCK\_OUTPUT\_标志在请求的**Flags**成员中设置\_ACK\_"请求的标志"\_输出\_[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)的*lpOutBuffer*参数。\_ 同样， [**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)可用于从内核模式确认 Windows 7 oplock。 有关详细信息，请参阅[**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)。

相关的 FSCTL 代码是 FSCTL\_OPLOCK\_中断\_通知。 如果调用方想要在给定流上的 oplock 中断完成时收到通知，则使用此代码。 此调用可能会阻止。 当 FSCTL\_OPLOCK\_BREAK\_通知调用返回状态\_成功时，这表示下列内容之一：

-   未授予 oplock。

-   调用时没有正在进行的 oplock 中断。

-   现在已完成任何正在进行的 oplock 中断。

若要在不需要确认时发送确认，则为错误，确认 FSCTL IRP 失败，状态\_无效的\_OPLOCK\_协议。

如果关闭请求 oplock 中断的文件的句柄，则会隐式确认中断。 对于共享冲突的 oplock 中断，oplock 持有者可以关闭文件句柄，该句柄可确认 oplock 中断，并防止文件的其他用户发生共享冲突。

 

 




