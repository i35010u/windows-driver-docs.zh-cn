---
title: Bug 检查 0xC9 DRIVER_VERIFIER_IOMANAGER_VIOLATION
description: DRIVER_VERIFIER_IOMANAGER_VIOLATION bug 检查具有 0x000000C9 值。 这是 bug 检查代码的所有驱动程序验证程序 I/O 验证冲突。
ms.assetid: dcafb0df-cbc1-44f4-8ec4-976df0842f0c
keywords:
- Bug 检查 0xC9 DRIVER_VERIFIER_IOMANAGER_VIOLATION
- DRIVER_VERIFIER_IOMANAGER_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_IOMANAGER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e7f31d1f9c4dcf46b51cd462a5432d015334b4e
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238558"
---
# <a name="bug-check-0xc9-driververifieriomanagerviolation"></a>Bug 检查 0xC9：驱动程序\_VERIFIER\_IOMANAGER\_冲突


该驱动程序\_VERIFIER\_IOMANAGER\_冲突错误检查的值为 0x000000C9。 这是所有驱动程序验证程序的 bug 检查代码**I/O 验证**冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="driververifieriomanagerviolation-parameters"></a>驱动程序\_VERIFIER\_IOMANAGER\_冲突参数


当驱动程序验证程序处于活动状态并**I/O 验证**是选择，各种 I/O 冲突将导致发出此 bug 检查。 参数 1 标识冲突的类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>要释放的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试释放的对象的类型不是 IO_TYPE_IRP 驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>要释放的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序尝试以释放 IRP 仍与线程相关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>IRP 发送的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序传递<strong>IoCallDriver</strong>不等于 IRP_TYPE IRP 类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序传递<strong>IoCallDriver</strong>无效设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>与有问题关联的设备对象的地址驱动程序</p></td>
<td align="left"><p>之前的 IRQL <strong>IoCallDriver</strong></p></td>
<td align="left"><p>之后的 IRQL <strong>IoCallDriver</strong></p></td>
<td align="left"><p>在对驱动程序调度例程的调用过程中更改的 IRQL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>IRP 状态</p></td>
<td align="left"><p>正在完成的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序调用<strong>IoCompleteRequest</strong>状态标记为挂起 （或等于-1）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>取消例程的地址</p></td>
<td align="left"><p>正在完成的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序调用<strong>IoCompleteRequest</strong>时仍将其取消例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>IRP 主要函数代码</p></td>
<td align="left"><p>异常状态代码</p></td>
<td align="left"><p>该驱动程序传递<strong>IoBuildAsynchronousFsdRequest</strong>缓冲区无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>I/O 控制代码</p></td>
<td align="left"><p>异常状态代码</p></td>
<td align="left"><p>该驱动程序传递<strong>IoBuildDeviceIoControlRequest</strong>缓冲区无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>IoCallDriver 调用 DISPATCH_LEVEL 上方。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>驱动程序快速 I/O 调度例程地址</p></td>
<td align="left"><p>然后再调用驱动程序调度例程的 IRQL</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>IoCallDriver 调用 DISPATCH_LEVEL 上方。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x12</p></td>
<td align="left"><p>驱动程序调度例程地址</p></td>
<td align="left"><p>然后再调用驱动程序调度例程的 IRQL</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>IoCallDriver 调用 DISPATCH_LEVEL 上方。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序传递<strong>最好</strong>具有一个已初始化计时器的设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>I/O 状态块的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序传递到 IRP，I/O 状态块，但具有已展开的时间之前的堆栈上分配此块。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>用户事件对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序传递到 IRP，用户事件，但在具有已展开的时间之前的堆栈上分配此事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>该驱动程序调用<strong>IoCompleteRequest</strong> IRQL 与&gt;DISPATCH_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>向其发送 IRP 的设备对象的地址</p></td>
<td align="left"><p>指向 IRP</p></td>
<td align="left"><p>指向文件对象的指针</p></td>
<td align="left"><p>该驱动程序发送的已关闭，或必须取消其打开的文件的对象的创建请求。</p></td>
</tr>
</tbody>
</table>

 

除了上表中所述的错误，有大量**I/O 验证**错误，导致驱动程序验证程序来暂停系统，但这不是实际的 bug 检查。

这些错误会导致在蓝色屏幕上，在崩溃转储文件，并在内核调试器中显示的消息。 这些消息将以不同的方式出现在这两个位置。 十六进制错误检查代码 0xC9 和 bug 出现这些错误时，检查字符串驱动程序\_VERIFIER\_IOMANAGER\_冲突不会显示在蓝色屏幕上或在调试器中，尽管它们将显示在崩溃转储文件.

在蓝色屏幕上，将显示以下数据：

-   消息**IO 系统验证错误**。

-   消息**WDM 驱动程序错误** *XXX*，其中*XXX*是表示特定错误的十六进制代码。 （请参阅下表中的 I/O 错误代码及其含义的列表。）

-   导致错误的驱动程序的名称。

-   其中的错误为驱动程序的代码中的地址检测到 (参数 2)。

-   指向 IRP (参数 3) 的指针。

-   指向设备对象 (参数 4) 的指针。

如果启用内核模式崩溃转储，故障转储文件中将显示以下信息：

-   消息**检测错误 0xC9 (驱动程序\_VERIFIER\_IOMANAGER\_冲突)**。

-   十六进制的 I/O 错误代码。 （请参阅下表中的 I/O 错误代码及其含义的列表。）

-   检测到错误的驱动程序的代码中的地址。

-   指向 IRP 的指针。

-   指向设备对象的指针。

如果内核调试程序附加到此冲突导致的系统，以下信息将发送到调试器：

-   消息**WDM 驱动程序错误**，以及错误的严重级别的评估。

-   导致错误的驱动程序的名称。

-   一个描述性字符串，其中介绍了此错误的原因。 通常附加信息传递，如指向 IRP 的指针。 （请参阅下表以了解这些描述性字符串和指定哪些附加信息的列表。）

-   针对执行进一步的操作的查询。 可能的响应都**b** （中断），**我**（忽略）， **z** (zap)， **r** （删除），或**d** （禁用）。 指示操作系统以继续，可看到会发生什么情况"down 行"如果此错误不发生。 当然，这通常会导致其他错误检查的执行。 "Zap"选项将实际删除导致此错误，要发现的断点。

**请注意**  无其他 bug 检查可以忽略这种方式。 仅这种类型的**I/O 验证**可以忽略错误，并附加了内核调试器情况下，才可以忽略这些错误。

 

下表列出了那些**I/O 验证**可以出现的错误。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">I/O 错误代码</th>
<th align="left">严重性</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>Unknown</p></td>
<td align="left"><p>此代码涵盖所有未知<strong>I/O 验证</strong>错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x201</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>设备正在其下的驱动程序堆栈中的另一台设备时删除本身。 这可能是因为忘记了调用方调用<strong>IoDetachDevice</strong>第一个或较低的驱动程序可能已错误地删除本身。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x202</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已尝试从未附加到任何一个设备对象分离。 如果可能出现此问题分离两次在同一个设备对象上调用。 （设备指定的对象。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x203</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已调用<strong>IoCallDriver</strong>而无需设置在取消例程中到 IRP <strong>NULL</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x204</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方已通过在<strong>NULL</strong>作为设备对象。 这是致命的。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x205</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方转发 IRP 当前排队等待其下。 处理 Irp 返回 STATUS_PENDING 中此驱动程序的代码看起来会被破坏。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x206</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方已正确转发 IRP （控制字段不归零）。 该驱动程序应使用<strong>IoCopyCurrentIrpStackLocationToNext</strong>或<strong>IoSkipCurrentIrpStackLocation</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x207</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方已手动复制到堆栈，并会无意中复制较高层完成例程。 该驱动程序应使用<strong>IoCopyCurrentIrpStackLocationToNext</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x208</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>此 IRP 即将耗尽堆栈位置。 有人可能已将转发此 IRP 从另一个堆栈。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x209</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方正在完成当前正在其下排队 IRP。 处理 Irp 返回 STATUS_PENDING 中此驱动程序的代码看起来会被破坏。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20A</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方<strong>IoFreeIrp</strong>释放仍在使用 IRP。 （原始 IRP 和中使用指定的 IRP。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20B</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方<strong>IoFreeIrp</strong>释放仍在使用 IRP。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20C</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方<strong>IoFreeIrp</strong>释放仍在对一个线程排队 IRP。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20D</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方<strong>IoInitializeIrp</strong>已通过使用已分配的 IRP <strong>IoAllocateIrp</strong>。 这是合法，并且不必要的并且导致配额泄漏。 查看文档，了解<strong>IoReuseIrp</strong>如果回收此 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20E</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>PNP IRP 具有无效的状态。 （任何 PNP IRP 必须初始化为 STATUS_NOT_SUPPORTED 其状态。）(指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20F</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>Power IRP 具有无效的状态。 （任何 Power IRP 必须初始化为 STATUS_NOT_SUPPORTED 其状态。）(指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x210</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>WMI IRP 具有无效的状态。 （任何 WMI IRP 必须初始化为 STATUS_NOT_SUPPORTED 其状态。）(指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x211</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已转发 IRP，并跳过在堆栈中的设备对象。 调用方可能将 Irp 发送到返回的设备而不是 PDO <strong>IoAttachDeviceToDeviceStack</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x212</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已放入回收站或不正确复制 IRP 的堆栈。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x213</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已更改并不了解的 IRP 的状态字段。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x214</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已更改并不了解的 IRP 的信息字段。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x215</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>正在关闭堆栈传递 IRP_MJ_PNP 非成功非的-STATUS_NOT_SUPPORTED IRP 状态。 (指定的 IRP。)失败的 PNP Irp，必须完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x216</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>先前设置 IRP_MJ_PNP 状态已转换为 STATUS_NOT_SUPPORTED。 (指定的 IRP。)此故障状态是由操作系统保留供使用。 驱动程序不能故障与该值 PnP IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x217</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>该驱动程序具有未处理所需的 IRP。 该驱动程序必须更新以指示已处理 IRP 的状态。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x218</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>该驱动程序已答复了 IRP 为其他位置堆栈中其他设备对象保留的。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x219</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>正在关闭堆栈传递 IRP_MJ_POWER 非成功非的-STATUS_NOT_SUPPORTED IRP 状态。 (指定的 IRP。)必须完成失败的 POWER Irp。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x21A</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>先前设置 IRP_MJ_POWER 状态已转换为 STATUS_NOT_SUPPORTED。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21B</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序返回可疑状态。 这可能是由于驱动程序中未初始化变量 bug。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x21C</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>调用方具有复制 IRP 堆栈，但未设置完成例程。 这会降低效率--请使用<strong>IoSkipCurrentIrpStackLocation</strong>相反。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21D</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>从其下收到删除 IRP 的堆栈中 IRP 调度处理程序具有不正确分离。 （设备对象、 调度例程和指定的 IRP。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x21E</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>IRP 调度处理程序未正确删除收到删除 IRP 其设备对象。 （设备对象、 调度例程和指定的 IRP。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21F</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序未填写完所需的 IRP 主要函数的调度例程。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x220</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>IRP_MJ_SYSTEM_CONTROL ProviderId 之外的某个已完成。 此 IRP 应或者之前完成，或应向下传递。 (IRP 与目标位置的设备对象一起指定。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x221</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>PDO 的 IRP 调度处理程序已删除其设备对象，但不是作为总线关系查询中缺少报告硬件。 （设备对象、 调度例程和指定的 IRP。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x222</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>收到删除 IRP PDO 时仍处于活动状态后已分离总线筛选器的 IRP 调度处理程序。 总线筛选器必须中清理<strong>FastIoDetach</strong>回调。 （设备对象、 调度例程和指定的 IRP。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x223</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>总线筛选器的 IRP 调度处理程序已删除其设备对象，但 PDO 仍然存在。 总线筛选器必须中清理<strong>FastIoDetach</strong>回调。 （设备对象、 调度例程和指定的 IRP。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x224</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>IRP 调度处理程序返回与 IRP 的不一致状态<strong>IoStatus.Status</strong>字段。 （调度处理程序例程，IRP，IRP 的 IoStatus.Status，并返回指定的状态。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x225</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>IRP 调度处理程序返回是非法的状态 (0xFFFFFFFF)。 这可能是因为未初始化的堆栈变量。 若要调试此错误，请使用<strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln （列表最接近符号）</a></strong>命令使用指定的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x226</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>IRP 调度处理程序返回而无需向下传递或完成此 IRP，或者在有人忘记返回 STATUS_PENDING。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x227</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>在代码中可分页的 IRP 完成例程。 （这是永远不会允许的。）(例程和指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x228</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序的完成例程未标记为挂起的 if IRP <strong>PendingReturned</strong> IRP 传递给它中设置了字段。 这可能导致 Windows 挂起，尤其是当堆栈返回错误。 (例程和指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x229</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>已为可能任意破坏其在取消例程在堆栈中较低的驱动程序当前正在处理 IRP 设置了取消例程。 (例程和指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22A</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>所需的 IRP 未响应的物理设备对象 (PDO)。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x22B</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>忘记了物理设备对象 (PDO) 填写设备的关系列表，并为 PDO <strong>TargetDeviceRelation</strong>查询。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22C</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>代码实现<strong>TargetDeviceRelation</strong>但调用查询<strong>ObReferenceObject</strong> PDO 上。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x22D</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已完成 IRP_MJ_PNP 它并不理解而不是向下传递。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22E</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已完成而不是向下传递成功 IRP_MJ_PNP。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x22F</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已完成 （而不是向下传递 IRP），保持不变的 IRP_MJ_PNP 或非 PDO 失败 IRP 使用 STATUS_NOT_SUPPORTED 的非法值。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x230</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已完成 IRP_MJ_POWER 它并不理解而不是向下传递。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x231</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>调用方已完成而不是向下传递成功 IRP_MJ_POWER。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x232</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已完成 （而不是向下传递 IRP），保持不变的 IRP_MJ_POWER 或非 PDO 失败 IRP 使用 STATUS_NOT_SUPPORTED 的非法值。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x233</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>未正确初始化 IRP 的查询功能中的查询功能结构版本字段中。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x234</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>未正确初始化 IRP 的查询功能中的查询功能结构的大小字段中。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x235</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>为-1 未正确初始化 IRP 的查询功能中的查询功能结构地址字段。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x236</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>为-1 未正确初始化 IRP 的查询功能中的查询功能结构 UI 数字字段。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x237</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序发送了受限制，仅供系统使用 IRP。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x238</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>调用方<strong>IoInitializeIrp</strong>已通过使用已分配的 IRP <strong>IoAllocateIrp</strong>。 这是非法的不必要的并且在正常使用的性能有负面影响。 如果正在回收此 IRP，请参阅<strong>IoReuseIrp</strong> Windows 驱动程序工具包中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x239</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>调用方<strong>IoCompleteRequest</strong> IRP 永远不会通过调用转发的完成<strong>IoCallDriver</strong>或<strong>PoCallDriver</strong>。 这可能是一个 bug。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x23A</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已转发对于此主要代码是非法的 IRQL 在 IRP。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23B</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已更改并不了解的 IRP 的状态字段。 (指定的 IRP。)</p></td>
</tr>
</tbody>
</table>

 

下表列出了其他**I/O 验证**可以出现的错误。 其中一些错误将仅会陆续披露如果**增强的 I/O 验证**激活。 在 Windows Vista 及更高版本，**增强的 I/O 验证**设置不作为的一部分**I/O 验证**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">I/O 错误代码</th>
<th align="left">严重性</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x23C</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已完成而无需设置在取消例程中到 IRP IRP <strong>NULL</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23D</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已返回 STATUS_PENDING 但未标记通过调用挂起的 IRP <strong>IoMarkIrpPending</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x23E</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已标记为挂起的 IRP，但未返回 STATUS_PENDING。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23F</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已经不会继承它已附加到的堆栈 DO_POWER_PAGABLE 位。 （设备指定的对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x240</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序尝试删除已删除通过以前调用的设备对象<strong>IoDeleteDevice</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x241</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已在意外删除 IRP 过程分离其设备对象。 （IRP 和设备指定的对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x242</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已在意外删除 IRP 期间删除其设备对象。 （IRP 和设备指定的对象。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x243</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序无法清除 DO_DEVICE_INITIALIZING 标志的末尾<strong>AddDevice</strong>。 （设备指定的对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x244</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已不会复制 DO_BUFFERED_IO 或 DO_DIRECT_IO 标志从附加到的设备对象。 （设备指定的对象。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x245</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>DO_BUFFERED_IO 和 DO_DIRECT_IO 标志已设置了驱动程序。 这些标志是互斥的。 （设备指定的对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x246</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序无法将复制<strong>DeviceType</strong>字段从附加到的设备对象。 （设备指定的对象。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x247</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序失败 IRP，不能合法失败。 (指定的 IRP。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x248</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序添加了不到设备的关系查询 PDO 的设备对象。 （IRP 和设备指定的对象。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x249</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序具有枚举返回相同的设备 Id 的两个子 PDOs。 （这两个指定设备对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24A</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序错误地调用了文件 I/O 函数使用 IRQL 不等于 passive_level 调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x24B</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序已完成类型的 IRP_MN_QUERY_DEVICE_RELATIONS 请求<strong>TargetDeviceRelation</strong>成功，但未正确未请求，请填写或转发到基础硬件堆栈 IRP。 （设备指定的对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24C</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已返回 STATUS_PENDING 但未通过调用标记挂起的 IRP <strong>IoMarkIrpPending</strong>。 (指定的 IRP。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x24D</p></td>
<td align="left"><p>致命错误</p></td>
<td align="left"><p>驱动程序需要 PDO 的函数传递一个无效的设备对象。 （设备指定的对象。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x300</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序返回可疑状态。 这可能是由于驱动程序中未初始化变量 bug。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x301</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已转发的 IRQL 在 IRP &gt; DISPATCH_LEVEL。 （指定的 IRQL 值）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x302</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已转发的 IRQL 在 IRP &gt;= APC_LEVEL。</p>
<p>I/O 管理器将需要队列 APC 来完成此请求。 APC 不能运行，因为调用方已在 APC 级别，因此调用方可能出现死锁。 （指定的 IRQL 值）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>该驱动程序正在完成 IRP_MJ_PNP （主要） 和 IRP_MN_REMOVE_DEVICE （次要） 请求失败状态代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x307</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>该驱动程序发出的 I/O 请求与已发出信号，并收到 STATUS_PENDING 响应的事件。 这可能导致 I/O 完成之前展开。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x310</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>该驱动程序重新初始化 IRP，仍在使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x311</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>该驱动程序重新初始化 IRP IoMakeAssociatedIrp、 IoBuildAsynchronousFsdRequest、 IoBuildSynchronousFsdRequest、 IoBuildDeviceIoControlRequest 通过使用创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x312</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方提供的 IRP 状态信息字段大于系统缓冲区的输出部分的值。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

请参阅每个代码的原因说明的 Parameters 节中的说明。

<a name="resolution"></a>分辨率
----------

当驱动程序验证程序已指示，若要监视一个或多个驱动程序时，才会发生此错误检查。 如果您不打算使用驱动程序验证程序，应停用它。 您可以考虑删除该驱动程序导致此问题。

如果你是驱动程序编写器，使用通过此 bug 检查获取的信息以在代码中修复的错误。

有关驱动程序验证程序的完整详细信息，请参阅 Windows 驱动程序工具包。

 

 




