---
title: Bug 检查 0xC9 DRIVER_VERIFIER_IOMANAGER_VIOLATION
description: DRIVER_VERIFIER_IOMANAGER_VIOLATION bug 检查的值为0x000000C9。 这是所有驱动程序验证程序 i/o 验证冲突的 bug 检查代码。
keywords:
- Bug 检查 0xC9 DRIVER_VERIFIER_IOMANAGER_VIOLATION
- DRIVER_VERIFIER_IOMANAGER_VIOLATION
ms.date: 05/07/2019
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_IOMANAGER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b29e44532ff729dc0fffa39fcde14c01d9cb3b67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825231"
---
# <a name="bug-check-0xc9-driver_verifier_iomanager_violation"></a>Bug 检查0xC9：驱动程序 \_ 验证程序 \_ IOMANAGER \_ 冲突

驱动程序 \_ 验证器 \_ IOMANAGER \_ 冲突 bug 检查的值为0x000000C9。 这是所有驱动程序验证程序 **I/o 验证** 冲突的 bug 检查代码。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="driver_verifier_iomanager_violation-parameters"></a>驱动程序 \_ 验证器 \_ IOMANAGER \_ 冲突参数

当驱动程序验证程序处于活动状态且选择了 **I/o 验证** 时，各种 i/o 冲突将导致发出此 bug 检查。 参数1标识冲突类型。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>正在释放的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序尝试释放其类型不 IO_TYPE_IRP 的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>正在释放的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序尝试释放仍与线程关联的 IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>正在发送的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序已通过 <strong>IoCallDriver</strong> 的 IRP 类型不等于 IRP_TYPE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序通过 <strong>IoCallDriver</strong> 的设备对象无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>与违犯的驱动程序相关联的设备对象的地址</p></td>
<td align="left"><p><strong>IoCallDriver</strong>之前的 IRQL</p></td>
<td align="left"><p><strong>IoCallDriver</strong>后的 IRQL</p></td>
<td align="left"><p>在对驱动程序调度例程的调用过程中，IRQL 发生变化。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>IRP 状态</p></td>
<td align="left"><p>要完成的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>名为 <strong>IoCompleteRequest</strong> 的驱动程序的状态标记为挂起 (或等于-1) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>取消例程的地址</p></td>
<td align="left"><p>要完成的 IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>在仍设置了其 cancel 例程的情况下，驱动程序调用 <strong>IoCompleteRequest</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>IRP 主要功能代码</p></td>
<td align="left"><p>异常状态代码</p></td>
<td align="left"><p><strong>IoBuildAsynchronousFsdRequest</strong>传递的驱动程序无效缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>I/o 控制代码</p></td>
<td align="left"><p>异常状态代码</p></td>
<td align="left"><p><strong>IoBuildDeviceIoControlRequest</strong>传递的驱动程序无效缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>DISPATCH_LEVEL 上调用了 IoCallDriver。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>驱动程序快速 i/o 调度例程地址</p></td>
<td align="left"><p>调用驱动程序调度例程之前的 IRQL</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>DISPATCH_LEVEL 上调用了 IoCallDriver。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x12</p></td>
<td align="left"><p>驱动程序调度例程地址</p></td>
<td align="left"><p>调用驱动程序调度例程之前的 IRQL</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>DISPATCH_LEVEL 上调用了 IoCallDriver。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>设备对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序通过已初始化的计时器 <strong>IoInitializeTimer</strong> 设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>I/o 状态块的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序将 i/o 状态块传递给 IRP，但此块是在已越过该点的堆栈上分配的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>用户事件对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序向 IRP 传递了一个用户事件，但是此事件是在已超出该点的堆栈上分配的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>IRP 的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>名为 <strong>IoCompleteRequest</strong> 的驱动程序 &gt; DISPATCH_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>要向其发送 IRP 的设备对象的地址</p></td>
<td align="left"><p>指向 IRP 的指针</p></td>
<td align="left"><p>指向文件对象的指针</p></td>
<td align="left"><p>驱动程序使用已关闭的文件对象发送了创建请求，或已将其打开取消。</p></td>
</tr>
</tbody>
</table>

 

除了上表中提到的错误之外，还有许多 **I/o 验证** 错误将导致驱动程序验证程序停止系统，但这并不是实际的 bug 检查。

这些错误会导致消息显示在蓝屏、崩溃转储文件和内核调试器中。 这些消息将以不同的方式在每个位置显示。 如果发生这些错误，则不会在蓝屏或调试器中显示十六进制 bug 检查代码0xC9 和 bug 检查字符串驱动程序 \_ 验证程序 \_ IOMANAGER \_ 冲突，尽管它们将出现在故障转储文件中。

在蓝屏上，将显示以下数据：

- 消息 **IO 系统验证错误**。

- 消息 **WDM 驱动程序错误** *XXX*，其中 *XXX* 是表示特定错误的十六进制代码。  (参阅下表，了解 i/o 错误代码及其含义的列表 ) 

- 导致错误的驱动程序的名称。

- 通常，驱动程序代码中检测到错误的地址 (参数 2) 。

如果已启用内核模式故障转储，则故障转储文件中将显示以下信息：

- 消息 **错误检查 0xC9 (DRIVER \_ VERIFIER \_ IOMANAGER \_ 冲突)**。

- 十六进制 i/o 错误代码。  (参阅下表，了解 i/o 错误代码及其含义的列表 ) 

- 通常，驱动程序代码中检测到错误的地址 (参数 2) 。

如果将内核调试器附加到导致此冲突的系统，则会将以下信息发送到调试器：

- 消息 **WDM 驱动程序错误**，以及对错误严重性的评估。

- 导致错误的驱动程序的名称。

- 说明导致此错误的原因的描述性字符串。 通常会传递附加信息，例如指向 IRP 的指针或指向设备对象或 IRQL 信息的指针。  (参阅下表以获取这些描述性字符串的列表以及指定的其他信息。 ) 

- 用于进一步操作的查询。 可能的响应为 **b** (break) ， **我** (忽略) ， **z** (zap) ， **r** (删除) 或 **d** (禁用) 。 指示操作系统继续，使您可以查看如果未发生此错误，将会出现什么情况。 当然，这通常会导致额外的 bug 检查。 "Zap" 选项将实际删除导致发现此错误的断点。

**注意**   不能以这种方式忽略其他 bug 检查。 只有此类 **I/o 验证** 错误可以忽略，甚至在附加了内核调试器的情况下，才能忽略这些错误。

下表列出了可能出现的这些 **I/o 验证** 错误。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">I/o 错误代码</th>
<th align="left">严重性</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>未知</p></td>
<td align="left"><p>此代码涵盖所有未知 <strong>I/o 验证</strong> 错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x201</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>当驱动程序堆栈中存在另一个设备时，该设备会将其删除。 这可能是因为调用方事先忘记了调用 <strong>IoDetachDevice</strong> ，或者低级驱动程序可能错误地删除了自身。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x202</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序尝试从未附加到任何内容的设备对象分离。 如果在同一设备对象上调用了两次分离，则可能会发生这种情况。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-设备对象地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x203</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已调用 <strong>IoCallDriver</strong> ，但未将 IRP 中的 cancel 例程设置为 <strong>NULL</strong>。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x204</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>调用方已作为设备对象传入 <strong>NULL</strong> 。 这是致命的。 </p>
<p>参数 2-保留</p>
<p>参数 3-保留</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x205</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>调用方正在转发当前在其下排队的 IRP。 在此驱动程序中返回 STATUS_PENDING 的代码处理 Irp 似乎已损坏。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x206</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>调用方错误地将 IRP (控制字段转发到了未归零) 。 驱动程序应使用 <strong>IoCopyCurrentIrpStackLocationToNext</strong> 或 <strong>IoSkipCurrentIrpStackLocation</strong>。</p>
<p>参数 2-保留</p>
<p>参数 3-保留</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x207</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>调用方已手动复制堆栈，并且无意中复制了上层的完成例程。 驱动程序应使用 <strong>IoCopyCurrentIrpStackLocationToNext</strong>。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x208</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>此 IRP 即将用尽堆栈位置。 有人可能从另一堆栈转发了此 IRP。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x209</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>调用方正在完成当前在其下排队的 IRP。 在此驱动程序中返回 STATUS_PENDING 的代码处理 Irp 似乎已损坏。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x20A</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p><strong>IoFreeIrp</strong>的调用方正在释放仍在使用的 IRP。 </p>
<p>参数 2-保留</p>
<p>参数 3-保留</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x20B</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p><strong>IoFreeIrp</strong>的调用方正在释放仍在使用的 IRP。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x20C</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p><strong>IoFreeIrp</strong>的调用方正在释放仍在线程上排队的 IRP。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x20D</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p><strong>IoInitializeIrp</strong>的调用方已通过<strong>IOALLOCATEIRP</strong>分配了 IRP。 这是非法的且不必要，导致了配额泄漏。 如果正在回收此 IRP，请查看 <strong>IoReuseIrp</strong> 的文档。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x20E</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>PNP IRP 具有无效状态。  (任何 PNP IRP 都必须将其状态初始化为 STATUS_NOT_SUPPORTED。 )  </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x20F</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>Power IRP 具有无效状态。  (任何电源 IRP 都必须将其状态初始化为 STATUS_NOT_SUPPORTED。 )  </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。 </p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x210</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>WMI IRP 具有无效状态。  (任何 WMI IRP 都必须将其状态初始化为 STATUS_NOT_SUPPORTED。 )  </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x211</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方在跳过堆栈中的设备对象时转发了 IRP。 调用方可能会将 Irp 发送到 PDO，而不是发送到 <strong>IoAttachDeviceToDeviceStack</strong>返回的设备。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x212</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方具有放入回收站或未正确复制 IRP 的堆栈。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x213</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已更改其不理解的 IRP 的 "状态" 字段。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x214</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已更改其不理解的 IRP 的信息字段。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x215</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>向下传递堆栈的 IRP_MJ_PNP 的非成功的非 STATUS_NOT_SUPPORTED IRP 状态。  无法完成 PNP Irp。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x216</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>之前设置的 IRP_MJ_PNP 状态已转换为 STATUS_NOT_SUPPORTED。  此失败状态保留给操作系统使用。 驱动程序无法通过此值使 PnP IRP 失败。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x217</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序未处理所需的 IRP。 驱动程序必须更新 IRP 的状态，以指示是否已对其进行处理。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x218</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已对为堆栈中其他位置的其他设备对象保留的 IRP 做出了响应。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x219</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>向下传递堆栈的 IRP_MJ_POWER 的非成功的非 STATUS_NOT_SUPPORTED IRP 状态。  故障电源 Irp 必须已完成。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x21A</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>之前设置的 IRP_MJ_POWER 状态已转换为 STATUS_NOT_SUPPORTED。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x21B</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序返回了可疑状态。 这可能是由于驱动程序中的变量未初始化。 </p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x21C</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>调用方已复制 IRP 堆栈，但未设置完成例程。 这是低效的--请改用 <strong>IoSkipCurrentIrpStackLocation</strong> 。</p>
<p>参数 2-保留</p>
<p>参数 3-保留</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x21D</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>在收到删除 IRP 后，IRP 调度处理程序未正确地从其下的堆栈中分离。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x21E</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>IRP 调度处理程序在收到删除 IRP 时未正确删除其设备对象。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x21F</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>对于必需的 IRP 主要功能，驱动程序未填充调度例程。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x220</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>IRP_MJ_SYSTEM_CONTROL 已由 ProviderId 以外的其他人完成。 此 IRP 应已在前面完成，或应已向下传递。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-ProviderId。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x221</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>PDO 的 IRP 调度处理程序已删除其设备对象，但在总线关系查询中未将硬件报告为缺失。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x222</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>当 PDO 仍处于活动状态时，在接收到删除 IRP 后，总线筛选器的 IRP 调度处理程序已分离。 总线筛选器必须清理 <strong>FastIoDetach</strong> 回调。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x223</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>总线筛选器的 IRP 调度处理程序已删除其设备对象，但 PDO 仍然存在。 总线筛选器必须清理 <strong>FastIoDetach</strong> 回调。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x224</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>IRP 调度处理程序返回了与 IRP 的 <strong>IoStatus</strong> 字段不一致的状态。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-预期状态代码。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x225</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>IRP 调度处理程序返回 (0xFFFFFFFF) 中非法的状态。 这可能是由于未初始化的堆栈变量。 若要调试此错误，请使用 ln (列出包含指定地址的 <strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">最接近符号) </a></strong> 命令。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-状态代码。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x226</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>IRP 调度处理程序已返回，无需关闭或完成此 IRP，或者有人忘记了返回 STATUS_PENDING。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x227</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>IRP 完成例程位于可分页的代码中。  (不允许这样做。 ) </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x228</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>如果在传递给它的 IRP 中设置了 <strong>PendingReturned</strong> 字段，则驱动程序的完成例程未将 irp 标记为 "挂起"。 这可能会导致 Windows 挂起，尤其是堆栈返回错误时。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x229</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>已为 IRP 设置了取消例程，该 IRP 当前正在由堆栈中较低版本的驱动程序处理，可能 stomping 其取消例程。</p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x22A</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p> (PDO) 的物理设备对象尚未响应所需的 IRP。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x22B</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p> (PDO 的物理设备对象) 忘记用 PDO 为 <strong>TargetDeviceRelation</strong> 查询填写设备关系列表。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x22C</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>实现 <strong>TargetDeviceRelation</strong> 查询的代码未在 PDO 上调用 <strong>ObReferenceObject</strong> 。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x22D</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方完成了无法理解的 IRP_MJ_PNP，而不是向下传递。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x22E</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已成功完成 IRP_MJ_PNP，而不是向下传递。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x22F</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方 IRP_MJ_PNP (完成了不变的，而不是将 IRP 向下传递) ，或者非 PDO 使用了非法值 "STATUS_NOT_SUPPORTED"。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x230</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方完成了无法理解的 IRP_MJ_POWER，而不是向下传递。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x231</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>调用方已成功完成 IRP_MJ_POWER，而不是向下传递。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x232</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方 IRP_MJ_POWER (完成了不变的，而不是将 IRP 向下传递) ，或者非 PDO 使用了非法值 "STATUS_NOT_SUPPORTED"。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x233</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>查询功能 IRP 的 "版本" 字段未正确初始化。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x234</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>查询功能 IRP 的 "大小" 字段未正确初始化。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x235</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>查询功能 IRP 的 "地址" 字段未正确初始化为-1。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x236</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>查询功能 IRP 中查询功能结构的 "UI 编号" 字段未正确初始化为-1。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x237</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已发送 IRP，该 IRP 仅限系统使用。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x238</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p><strong>IoInitializeIrp</strong>的调用方已通过<strong>IOALLOCATEIRP</strong>分配了 IRP。 这是非法的、不必要的，并会对正常使用的性能产生负面影响。 如果正在回收此 IRP，请参阅 Windows 驱动程序工具包中的 <strong>IoReuseIrp</strong> 。</p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x239</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p><strong>IoCompleteRequest</strong>的调用方正在完成尚未通过调用<strong>IoCallDriver</strong>或<strong>PoCallDriver</strong>进行转发的 IRP。 这可能是一个 bug。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x23A</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已将 IRP 转发到对于此主要代码非法的 IRQL。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x23B</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方已更改其不理解的 IRP 的 "状态" 字段。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
</tbody>
</table>

下表列出了可能出现的其他 **I/o 验证** 错误。 当激活增强的 **I/o 验证** 时，将出现这些错误。 有关详细信息，请参阅 [增强型 I/o 验证](../devtest/enhanced-i-o-verification.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">I/o 错误代码</th>
<th align="left">严重性</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x23C</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已完成 IRP，但没有将 IRP 中的 "取消" 例程设置为 <strong>NULL</strong>。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x23D</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已 STATUS_PENDING 返回，但未通过调用 <strong>也</strong>将 IRP 标记为挂起。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-状态代码。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x23E</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已将 IRP 标记为 "已挂起"，但未返回 STATUS_PENDING。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-状态代码。 </p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x23F</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序没有从它所附加到的堆栈中继承 DO_POWER_PAGABLE 位。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x240</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序正在尝试删除已通过之前对 <strong>IoDeleteDevice</strong>的调用删除的设备对象。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x241</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>在意外删除 IRP 期间，驱动程序已分离其设备对象。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x242</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已在意外删除 IRP 期间删除了其设备对象。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x243</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序未能清除 <strong>AddDevice</strong>结尾的 DO_DEVICE_INITIALIZING 标志。</p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
<p>参数 4- </p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x244</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序没有从其附加到的设备对象复制 DO_BUFFERED_IO 或 DO_DIRECT_IO 标志。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x245</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序同时设置了 DO_BUFFERED_IO 和 DO_DIRECT_IO 标志。 这些标志互相排斥。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x246</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序无法从其附加到的设备对象复制 <strong>DeviceType</strong> 字段。 </p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x247</p></td>
<td align="left"><p>错误</p>
<p>参数 2-保留。</p>
<p>参数 3-已保留。</p>
</td>
<td align="left"><p>驱动程序失败，无法合法地失败的 IRP。 </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x248</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已向设备关系查询添加了不是 PDO 的设备对象。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x249</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已枚举两个子 PDOs，它们返回了相同的设备 Id。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-第一个设备对象地址。</p>
<p>参数 4-第二个设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x24A</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序错误地调用了不等于 PASSIVE_LEVEL 的文件 i/o 函数。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-已保留。</p>
<p>参数 4-已保留。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x24B</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序已成功完成 <strong>TargetDeviceRelation</strong> 类型的 IRP_MN_QUERY_DEVICE_RELATIONS 请求，但未正确填写请求或将 IRP 转发到基础硬件堆栈。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x24C</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已 STATUS_PENDING 返回，但未通过调用 <strong>也</strong>将 IRP 标记为挂起。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-状态代码。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x24D</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>驱动程序将无效设备对象传递到需要 PDO 的函数。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-设备对象地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x300</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序返回了可疑状态。 这可能是由于驱动程序中的变量未初始化。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-可疑状态代码。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x301</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已将 IRP 转发到 DISPATCH_LEVEL >。 </p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-错误值</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x302</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序已将 IRP 转发 > = APC_LEVEL。</p>
<p>I/o 管理器需要对 APC 进行排队才能完成此请求。 APC 将无法运行，因为调用方已在 APC 级别，因此调用方可能会死锁。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
<p>参数 4-IRQL 值不正确。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序正在完成 IRP_MJ_PNP (主要) ，并 IRP_MN_REMOVE_DEVICE (次使用失败状态代码的请求。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x307</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序发出 i/o 请求，其中事件已发出信号并收到 STATUS_PENDING 响应。 这可能会导致 i/o 完成。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x310</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序正在重新初始化仍在使用中的 IRP。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x311</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>驱动程序正在重新初始化使用 IoMakeAssociatedIrp、IoBuildAsynchronousFsdRequest、IoBuildSynchronousFsdRequest、IoBuildDeviceIoControlRequest 创建的 IRP。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x312</p></td>
<td align="left"><p>非致命错误</p></td>
<td align="left"><p>调用方提供的 IRP 状态信息字段的值大于系统缓冲区的输出部分。</p>
<p>参数 2-检测到错误的驱动程序代码中的地址。</p>
<p>参数 3-IRP 地址。</p>
</td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

有关原因的说明，请参阅参数部分中每个代码的说明。

<a name="resolution"></a>解决方法
----------

此 bug 检查只能在已指示驱动程序验证器监视一个或多个驱动程序时出现。 如果你不打算使用驱动程序验证程序，则应停用它。 有关详细信息，请参阅 [驱动程序验证程序](../devtest/driver-verifier.md)中的 "如何控制驱动程序验证程序"。 你可能会考虑更新或删除导致此问题的驱动程序。

如果您是驱动程序开发人员，请使用通过此 bug 检查获取的信息来修复代码中的 bug。

有关驱动程序验证程序的完整详细信息，请参阅 [驱动程序验证](../devtest/driver-verifier.md)器。
