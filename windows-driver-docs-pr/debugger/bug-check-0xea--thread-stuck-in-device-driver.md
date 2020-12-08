---
title: Bug 检查 0xEA THREAD_STUCK_IN_DEVICE_DRIVER
description: THREAD_STUCK_IN_DEVICE_DRIVER bug 检查的值为0x000000EA。 这表示设备驱动程序中的线程无休止地旋转。
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
ms.openlocfilehash: 2bd35da3c30c5a5aa3bda68fb73e29cd2d524e9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793255"
---
# <a name="bug-check-0xea-thread_stuck_in_device_driver"></a>Bug 检查0xEA：线程 \_ 停滞 \_ 在 \_ 设备 \_ 驱动程序中


线程 \_ 卡 \_ 在 \_ 设备 \_ 驱动程序 bug 检查中的值为0x000000EA。 这表示设备驱动程序中的线程无休止地旋转。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="thread_stuck_in_device_driver-parameters"></a>线程 \_ 停滞 \_ 在 \_ 设备 \_ 驱动程序参数中


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
<td align="left"><p>指向停滞线程对象的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>指向 DEFERRED_WATCHDOG 对象的指针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向有问题的驱动程序名称的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p><strong>在内核调试器中：</strong> 命中 "截获" bug 检查0xEA 的次数</p>
<p><strong>在蓝屏上：</strong> 1</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

设备驱动程序在无限循环中旋转，最有可能等待硬件进入空闲状态。

这通常表示硬件本身有问题，或者设备驱动程序对硬件的编程不正确。 通常，这是由于视频卡损坏或显示器驱动程序错误导致的。

<a name="resolution"></a>解决方法
----------

使用 [**. thread (设置 Register Context)**](-thread--set-register-context-.md) 命令以及参数1。 然后，使用 [**kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 查找线程停滞的位置。

如果内核调试器已连接并且在 Windows 检测到超时情况时正在运行，则为。 然后，将调用 **DbgBreakPoint** 而不是 **KeBugCheckEx**。 详细消息将打印到调试器。 有关详细信息，请参阅 [向 Debugge 发送输出](sending-output-to-the-debugger.md)。

此消息将包含 bug 检查参数的内容。 由于未发出实际 bug 检查，因此 [**(显示 Bug 检查数据)**](-bugcheck--display-bug-check-data-.md) 命令将不起作用。 还可以通过在32位系统上使用 **dd 监视程序！ g \_ WdBugCheckData l5**"或在64位系统上使用 **dq 监视程序！ g \_ WdBugCheckData l5**" 从监视器的全局变量检索这四个参数。

以交互方式（如此错误）调试此错误将使你能够找到有问题的线程，在其中设置断点，然后使用 [**g (转)**](g--go-.md) 返回到旋转代码，以便进一步调试。

在 (OS 版本3790或更早) 版本的多处理器计算机上，如果旋转线程被硬件中断中断，并且 ISR 或 DPC 例程正在运行 bug 检查时，则可能会遇到超时。 这是因为超时的工作项可以在第二个 CPU 和同一时间进行传递和处理。 如果出现这种情况，则必须深入了解有问题的线程堆栈，确定导致超时的旋转代码。 使用 [**dds (显示单词和符号)**](dds--dps--dqs--display-words-and-symbols-.md) 命令执行此操作。

 

 




