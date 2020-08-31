---
title: 旧筛选器驱动程序移植指南
description: 旧筛选器驱动程序移植指南
ms.assetid: 6dd9637e-e9b3-4434-996c-c3f8ce6584c4
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，移植旧驱动程序
- 迁移旧筛选器驱动程序
- 旧筛选器驱动程序 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d48fbdd2b1cb16d4c102197b6635121798f7cb3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063354"
---
# <a name="guidelines-for-porting-legacy-filter-drivers"></a>旧筛选器驱动程序移植指南


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


鼓励开发人员将旧筛选器驱动程序移植到筛选器管理器模型，以便为其筛选器驱动程序获取更好的功能，并提高系统的可靠性。 经验丰富的开发人员会发现，将旧版筛选器驱动程序移植到微筛选器驱动程序相对简单。 Microsoft 筛选器驱动程序开发人员建议采用以下方法：

-   从可靠的回归测试套件开始，验证旧筛选器驱动程序和移植微筛选器驱动程序之间的行为。

-   创建微筛选器驱动程序 shell，并将功能从旧筛选器驱动程序系统上移至微筛选器驱动程序。 例如，获取连接工作，然后一次处理一个操作，每次操作后测试一次。

-   更改用户模式/内核模式通信最后，以便您可以使用现有工具来测试微筛选器驱动程序。

-   在启用了驱动程序验证器中的筛选器验证程序 i/o 验证选项的情况 PREfast 的情况编译和测试。

在迁移过程中，应查看所有旧筛选器驱动程序代码，以充分利用筛选器管理器功能。 具体而言，请记住以下事项：

-   基于 IRP 的 i/o 和快速 i/o 操作可以在适当的时候执行相同的操作，这有助于减少代码重复。

-   在注册操作时，微筛选器驱动程序可以明确选择忽略所有分页 i/o 和缓存 i/o，这样就无需对代码进行检查。

-   实例通知可大大简化附加/分离逻辑。

-   仅注册微筛选器驱动程序必须处理的操作;您可以忽略其他所有内容。

-   利用筛选器管理器上下文和名称管理支持。

-   利用筛选器管理器对发出非递归 i/o 的支持。

-   与旧版筛选器驱动程序不同，微筛选器驱动程序不能依赖于本地变量来维护从 preoperation 处理到 postoperation 处理的上下文。 请考虑分配后备链表列表以存储操作状态。

-   请确保在使用名称或上下文完成后释放引用。

-   用户模式下的完成端口添加了一种用于生成队列的强大技术。 您可能只需要与单个命名端口建立单一连接。

下表列出了旧筛选器驱动程序中的常见操作以及它们如何映射到筛选器管理器模型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旧筛选器驱动程序模型</th>
<th align="left">筛选器管理器模型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>无完成例程的传递操作</p></td>
<td align="left"><p>如果你的微筛选器驱动程序绝不能处理此类型的 i/o 操作，则不要为此操作注册 preoperation 或 postoperation 回调例程。</p>
<p>否则，请从为此操作注册的 preoperation 回调例程返回 FLT_PREOP_SUCCESS_NO_CALLBACK。</p>
<p>请参阅 <a href="returning-flt-preop-success-no-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_NO_CALLBACK](returning-flt-preop-success-no-callback.md)">返回 FLT_PREOP_SUCCESS_NO_CALLBACK</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用完成例程传递操作</p></td>
<td align="left"><p>从 preoperation 回调例程返回 FLT_PREOP_SUCCESS_WITH_CALLBACK。</p>
<p>请参阅 <a href="returning-flt-preop-success-with-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_WITH_CALLBACK](returning-flt-preop-success-with-callback.md)">返回 FLT_PREOP_SUCCESS_WITH_CALLBACK</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Preoperation 回调例程中的挂起操作</p></td>
<td align="left"><p>根据需要调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)"><strong>FltLockUserBuffer</strong></a> ，以确保所有用户缓冲区均已正确锁定，以便可以在工作线程中访问它们。</p>
<p>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem" data-raw-source="[&lt;strong&gt;FltAllocateDeferredIoWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)"><strong>FltAllocateDeferredIoWorkItem</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem" data-raw-source="[&lt;strong&gt;FltQueueDeferredIoWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)"><strong>FltQueueDeferredIoWorkItem</strong></a>等支持例程，将工作排队到工作线程中。</p>
<p>从 preoperation 回调例程返回 FLT_PREOP_PENDING。</p>
<p>准备好将 i/o 操作返回到筛选器管理器后，请调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)"><strong>FltCompletePendedPreOperation</strong></a>。</p>
<p>请参阅 <a href="pending-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Preoperation Callback Routine](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)">在 Preoperation 回调例程中挂起 I/o 操作</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Postoperation 回调例程中的挂起操作</p></td>
<td align="left"><p>在 preoperation 回调例程中调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)"><strong>FltLockUserBuffer</strong></a> ，以确保已正确锁定用户缓冲区以便可以在工作线程中访问它们。</p>
<p>通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem" data-raw-source="[&lt;strong&gt;FltAllocateGenericWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)"><strong>FltAllocateGenericWorkItem</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem" data-raw-source="[&lt;strong&gt;FltQueueGenericWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)"><strong>FltQueueGenericWorkItem</strong></a>等支持例程，将工作排队到工作线程中。</p>
<p>从 postoperation 回调例程返回 FLT_POSTOP_MORE_PROCESSING_REQUIRED。</p>
<p>准备好将 i/o 操作返回到筛选器管理器后，请调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPostOperation&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)"><strong>FltCompletePendedPostOperation</strong></a>。</p>
<p>请参阅 <a href="pending-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Postoperation Callback Routine](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)">在 Postoperation 回调例程中挂起 I/o 操作</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>同步操作</p></td>
<td align="left"><p>从 preoperation 回调例程返回 FLT_PREOP_SYNCHRONIZE。</p>
<p>请参阅 <a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">返回 FLT_PREOP_SYNCHRONIZE</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>在 preoperation 回调例程中完成操作</p></td>
<td align="left"><p>在操作的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>结构的<strong>IoStatus</strong>成员中设置最终操作状态和信息。</p>
<p>从 preoperation 回调例程返回 FLT_PREOP_COMPLETE。</p>
<p>请参阅 <a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">在 Preoperation 回调例程中完成 I/o 操作</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在 preoperation 回调例程中挂起操作后完成该操作</p></td>
<td align="left"><p>在操作的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>结构的<strong>IoStatus</strong>成员中设置最终操作状态和信息。</p>
<p>从处理 i/o 操作的工作线程调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)"><strong>FltCompletePendedPreOperation</strong></a> ，将 FLT_PREOP_COMPLETE 传递为 <em>CallbackStatus</em> 参数。</p>
<p>请参阅 <a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">在 Preoperation 回调例程中完成 I/o 操作</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>完成完成例程中的所有完成工作</p></td>
<td align="left"><p>从 postoperation 回调例程返回 FLT_POSTOP_FINISHED_PROCESSING。</p>
<p>请参阅 <a href="writing-postoperation-callback-routines.md" data-raw-source="[Writing Postoperation Callback Routines](writing-postoperation-callback-routines.md)">编写 Postoperation 回调例程</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在安全 IRQL 上完成工作</p></td>
<td align="left"><p>从 postoperation 回调例程调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe" data-raw-source="[&lt;strong&gt;FltDoCompletionProcessingWhenSafe&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)"><strong>FltDoCompletionProcessingWhenSafe</strong></a> 。</p>
<p>请参阅 <a href="ensuring-that-completion-processing-is-performed-at-safe-irql.md" data-raw-source="[Ensuring that Completion Processing is Performed at Safe IRQL](ensuring-that-completion-processing-is-performed-at-safe-irql.md)">确保在安全的 IRQL 处执行完成处理</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>向完成例程通知事件</p></td>
<td align="left"><p>从此操作的 preoperation 回调例程返回 FLT_PREOP_SYNCHRONIZE。</p>
<p>筛选器管理器将在与 preoperation 回调例程相同的线程上下文中调用 postoperation 回调例程，以 IRQL &lt; = APC_LEVEL。</p>
<p>请参阅 <a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">返回 FLT_PREOP_SYNCHRONIZE</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>未能成功创建操作</p></td>
<td align="left"><p>从 postoperation 回调例程调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen" data-raw-source="[&lt;strong&gt;FltCancelFileOpen&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)"><strong>FltCancelFileOpen</strong></a> ，以进行创建操作。</p>
<p>在操作<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>结构的<strong>IoStatus</strong>成员中设置相应的错误 NTSTATUS 值。</p>
<p>返回 FLT_POSTOP_FINISHED_PROCESSING。</p>
<p>请参阅 <a href="failing-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Failing an I/O Operation in a Postoperation Callback Routine](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)">Postoperation 回调例程中的 I/o 操作失败</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>通过 i/o 操作的快速 i/o 路径禁止 i/o</p></td>
<td align="left"><p>从 preoperation 回调例程返回 FLT_STATUS_DISALLOW_FAST_IO 操作。</p>
<p>请参阅 <a href="disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Disallowing a Fast I/O Operation in a Preoperation Callback Routine](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)">在 Preoperation 回调例程中禁用快速 I/o 操作</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>修改 i/o 操作的参数</p></td>
<td align="left"><p>在操作的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>结构的<strong>Iopb</strong>成员中设置修改后的参数值。</p>
<p>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty" data-raw-source="[&lt;strong&gt;FltSetCallbackDataDirty&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)"><strong>FltSetCallbackDataDirty</strong></a>，将 FLT_CALLBACK_DATA 结构标记为已更新，除非修改了 FLT_CALLBACK_DATA 结构的 <strong>IoStatus</strong> 成员的内容。</p>
<p>请参阅 <a href="modifying-the-parameters-for-an-i-o-operation.md" data-raw-source="[Modifying the Parameters for an I/O Operation](modifying-the-parameters-for-an-i-o-operation.md)">修改 I/o 操作的参数</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>锁定操作的用户缓冲区</p></td>
<td align="left"><p>使用在 <a href="accessing-the-user-buffers-for-an-i-o-operation.md" data-raw-source="[Accessing the User Buffers for an I/O Operation](accessing-the-user-buffers-for-an-i-o-operation.md)">访问 I/o 操作的用户缓冲区</a>中所述的技术和指导原则。</p></td>
</tr>
</tbody>
</table>

 

 

