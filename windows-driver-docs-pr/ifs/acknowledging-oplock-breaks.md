---
title: 确认 Oplock 分隔线
description: 确认 Oplock 分隔线
ms.assetid: ea5bcd1e-d22c-4f80-89e4-1a61e43959dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2aa2a988f24e33c145ad24d075f71f334751c7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555585"
---
# <a name="acknowledging-oplock-breaks"></a>确认 Oplock 分隔线


## <span id="oplock_break_conditions"></span><span id="OPLOCK_BREAK_CONDITIONS"></span>


有不同类型的机会锁的所有者可以返回的确认。 类似于[授予请求](granting-oplocks.md)，作为文件系统控制代码发送这些确认 (即[FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)s)。 它们是：

-   FSCTL\_OPLOCK\_中断\_确认
    -   此 FSCTL 指示 oplock 所有者已完成流同步，并且它们接受的级别 （级别 2 或无） 向其断开 oplock。
-   FSCTL\_OPLOCK\_BREAK\_ACK\_NO\_2
    -   此 FSCTL 指示 oplock 所有者已完成流同步，但不是希望级别 2 oplock。 相反，oplock 应为无中断 （即，oplock 是被放弃，完全）。
-   FSCTL\_OPBATCH\_ACK\_关闭\_PENDING
    -   对于级别 1 oplock，此 FSCTL 指示 oplock 所有者已完成流同步和完全释放适配器的 oplock （没有第二级 oplock，可能会导致这种确认）。

    <!-- -->

    -   对于批处理或筛选器的机会锁，此 FSCTL 指示 oplock 所有者想要关闭流句柄对授予 oplock。 操作被阻止，正在等待确认破坏 oplock，继续等待，直到关闭的机会锁所有者的句柄。
-   FSCTL\_REQUEST\_OPLOCK
    -   通过指定请求\_OPLOCK\_输入\_标志\_中的 ACK**标志**成员的请求\_OPLOCK\_输入\_缓冲区作为结构传递*lpInBuffer*的参数[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)，此 FSCTL 用于确认的 Windows 7 oplock 的分页符。 确认是必需的仅当请求\_OPLOCK\_输出\_标志\_ACK\_中设置了必需标志**标志**成员请求\_OPLOCK\_输出\_缓冲区结构作为传递*lpOutBuffer*参数的[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)。 以类似方式[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)并[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)可用于确认从内核模式的 Windows 7 oplock。 有关详细信息，请参阅[ **FSCTL\_请求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)。

一个相关 FSCTL 代码是 FSCTL\_OPLOCK\_中断\_通知。 当调用方想要在给定的流上破坏 oplock 完成时通知时使用此代码。 此调用可能会阻止。 当 FSCTL\_OPLOCK\_中断\_通知调用将返回状态\_成功时，这表示以下值之一：

-   没有授予 oplock。

-   在调用时，进度时没有破坏 oplock。

-   任何正在进行的破坏 oplock 现已完成。

发送的确认时应不发送任何确认是一个错误，并确认 FSCTL IRP 失败，状态\_无效\_OPLOCK\_协议。

关闭该文件为其请求需要破坏 oplock 句柄将隐式确认中断。 对于共享冲突 oplock，机会锁持有者可以关闭文件句柄，确认破坏 oplock，并阻止其他用户共享冲突的文件。

 

 




