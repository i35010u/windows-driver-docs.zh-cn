---
title: Bug 检查 0xEA THREAD_STUCK_IN_DEVICE_DRIVER
description: THREAD_STUCK_IN_DEVICE_DRIVER bug 检查具有 0x000000EA 值。 这表示无休止地旋转的设备驱动程序中的线程。
ms.assetid: f3d6acaf-3445-4fc3-b4ed-b72a74a32b57
keywords:
- Bug 检查 0xEA THREAD_STUCK_IN_DEVICE_DRIVER
- THREAD_STUCK_IN_DEVICE_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THREAD_STUCK_IN_DEVICE_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d256ccb687cc0004acf1dc80b9dc03e6270d026
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518783"
---
# <a name="bug-check-0xea-threadstuckindevicedriver"></a>Bug 检查 0xEA：THREAD\_STUCK\_IN\_DEVICE\_DRIVER


在线程\_STUCK\_IN\_设备\_驱动程序 bug 检查的值为 0x000000EA。 这表示无休止地旋转的设备驱动程序中的线程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="threadstuckindevicedriver-parameters"></a>线程\_STUCK\_IN\_设备\_驱动程序参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>指向受阻的线程对象的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>指向 DEFERRED_WATCHDOG 对象的指针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向有问题的驱动程序名称</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p><strong>在内核调试程序：</strong>点击"被拦截"的 bug 检查 0xEA 次数</p>
<p><strong>在蓝色屏幕：</strong>1</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

设备驱动程序旋转无限循环，很可能等待硬件变为空闲状态。

这通常表示硬件本身，或未正确编程硬件的设备驱动程序出现问题。 通常情况下，这是错误的视频卡或错误显示驱动程序的结果。

<a name="resolution"></a>分辨率
----------

使用[ **.thread （设置注册上下文）** ](-thread--set-register-context-.md)命令及参数 1。 然后，使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)来查找其中线程是否已卡住的位置。

如果内核调试器已连接并在运行时 Windows 检测到超时情况。 然后**DbgBreakPoint**将调用而不是**KeBugCheckEx**。 详细的消息将被打印到调试器。 请参阅[将输出发送到 Debugge](sending-output-to-the-debugger.md)有关详细信息。

此消息将包括已 bug 检查参数。 由于没有实际的 bug 检查已发布，所以[ **.bugcheck （显示 Bug 检查数据）** ](-bugcheck--display-bug-check-data-.md)命令将不起作用。 四个参数还通过监视程序的全局变量使用来检索**dd 监视器 ！ g\_WdBugCheckData L5**"在 32 位系统上，或者**dq 监视器 ！ g\_WdBugCheckData L5**"上的 64 位系统。

以交互方式调试此错误，如这将使您能够找到有问题的线程，设置断点，以及如何将[ **g （转向）** ](g--go-.md)以返回到旋转代码，以进一步调试。

在多处理器计算机 (OS build 3790 或更早版本)，可以按超时时间，如果，旋转线程被中断的硬件中断和 ISR 或 DPC 例程运行时错误检查。 这是因为可以传递并在第二个 CPU 和同时处理超时时间的工作项。 如果发生这种情况，你必须考虑在有问题的线程的堆栈，以确定导致超时时间发生的旋转代码更深入。 使用[ **（显示单词和符号） 的 dds** ](dds--dps--dqs--display-words-and-symbols-.md)命令来执行此操作。

 

 




