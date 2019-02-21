---
title: 对于移植旧筛选器驱动程序的指导原则
description: 对于移植旧筛选器驱动程序的指导原则
ms.assetid: 6dd9637e-e9b3-4434-996c-c3f8ce6584c4
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，将旧驱动程序移植
- 将旧的筛选器驱动程序移植
- 旧的筛选器驱动程序 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c0fa4298b205552d18ba98dff3a6d283491de0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540556"
---
# <a name="guidelines-for-porting-legacy-filter-drivers"></a>对于移植旧筛选器驱动程序的指导原则


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


建议为筛选器管理器模型以获得更好地为其筛选器驱动程序的功能并提高系统可靠性端口旧筛选器驱动程序的开发人员。 有经验的开发人员会发现它相对易于移植到微筛选器驱动程序的旧的筛选器驱动程序。 筛选器驱动程序开发人员在 Microsoft 建议使用以下方法：

-   开始使用可靠的回归测试套件，若要验证旧的筛选器驱动程序与已移植微筛选器驱动程序之间的行为。

-   创建微筛选器驱动程序命令行程序和系统地将功能从旧的筛选器驱动程序移动到微筛选器驱动程序。 例如，即可使用附件，然后端口一次操作时，每次操作后测试。

-   最后，更改用户模式/内核模式通信，因此可以使用现有的工具来测试微筛选器驱动程序。

-   使用 PREfast 编译和测试中启用的驱动程序验证程序的筛选器验证程序 I/O 验证选项。

在迁移过程中，应检查所有旧的筛选器驱动程序代码，以充分利用筛选器管理器功能。 具体而言，请记住以下：

-   基于 IRP 的 I/O 和快速的 I/O 操作可来自通过相同的操作时适当情况下，这有助于减少重复代码。

-   注册时的操作，可以显式选择微筛选器驱动程序忽略所有分页 I/O 和缓存的 I/O，从而消除了对代码以检查这些需要。

-   实例通知极大地简化附加/分离的逻辑。

-   仅注册微筛选器驱动程序必须处理; 的操作你可以忽略其他所有内容。

-   利用筛选器管理器上下文和名称管理支持。

-   利用筛选器发出非递归 I/O 管理器支持。

-   与旧的筛选器驱动程序，不同微筛选器驱动程序不能依赖于本地变量来维护从 preoperation 处理到 postoperation 处理上下文。 请考虑分配一个后备链列表来存储操作状态。

-   请确保释放时已完成，但名称或上下文的引用。

-   在用户模式下完成端口添加功能强大的技术，用于构建队列。 将可能需要单个连接到单个命名端口。

下表列出了旧的筛选器驱动程序以及它们如何映射到筛选器管理器模型中常见的操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旧的筛选器驱动程序模型</th>
<th align="left">筛选器管理器模型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>传递操作没有完成例程</p></td>
<td align="left"><p>如果永远不会微筛选器驱动程序不起作用的 I/O 操作此类型，则不需要注册此操作的 preoperation 或 postoperation 回调例程。</p>
<p>否则为返回 FLT_PREOP_SUCCESS_NO_CALLBACK preoperation 回调例程注册此操作。</p>
<p>请参阅<a href="returning-flt-preop-success-no-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_NO_CALLBACK](returning-flt-preop-success-no-callback.md)">返回 FLT_PREOP_SUCCESS_NO_CALLBACK</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>传递操作完成例程</p></td>
<td align="left"><p>返回 FLT_PREOP_SUCCESS_WITH_CALLBACK preoperation 回调例程。</p>
<p>请参阅<a href="returning-flt-preop-success-with-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_WITH_CALLBACK](returning-flt-preop-success-with-callback.md)">返回 FLT_PREOP_SUCCESS_WITH_CALLBACK</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Preoperation 回调例程中的挂起操作</p></td>
<td align="left"><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff543371" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543371)"> <strong>FltLockUserBuffer</strong> </a> ，以确保这样用户可以访问的工作线程中正确地锁定任何用户缓冲区。</p>
<p>队列到通过调用一个工作线程的工作支持例程，如<a href="https://msdn.microsoft.com/library/windows/hardware/ff541720" data-raw-source="[&lt;strong&gt;FltAllocateDeferredIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541720)"> <strong>FltAllocateDeferredIoWorkItem</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff543449" data-raw-source="[&lt;strong&gt;FltQueueDeferredIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543449)"> <strong>FltQueueDeferredIoWorkItem</strong> </a>.</p>
<p>返回 FLT_PREOP_PENDING preoperation 回调例程。</p>
<p>准备好返回到筛选器管理器的 I/O 操作后，调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff541913" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541913)"> <strong>FltCompletePendedPreOperation</strong></a>。</p>
<p>请参阅<a href="pending-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Preoperation Callback Routine](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)">挂起的 I/O 操作中 Preoperation 回调例程</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Postoperation 回调例程中的挂起操作</p></td>
<td align="left"><p>在 preoperation 回调例程中，调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff543371" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543371)"> <strong>FltLockUserBuffer</strong> </a>以确保该用户锁定了缓冲区正确，以便可以在辅助线程中访问它们。</p>
<p>队列到通过调用一个工作线程的工作支持例程，如<a href="https://msdn.microsoft.com/library/windows/hardware/ff541749" data-raw-source="[&lt;strong&gt;FltAllocateGenericWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541749)"> <strong>FltAllocateGenericWorkItem</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff543452" data-raw-source="[&lt;strong&gt;FltQueueGenericWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543452)"> <strong>FltQueueGenericWorkItem</strong> </a>.</p>
<p>返回 FLT_POSTOP_MORE_PROCESSING_REQUIRED postoperation 回调例程。</p>
<p>准备好返回到筛选器管理器的 I/O 操作后，调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff541897" data-raw-source="[&lt;strong&gt;FltCompletePendedPostOperation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541897)"> <strong>FltCompletePendedPostOperation</strong></a>。</p>
<p>请参阅<a href="pending-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Postoperation Callback Routine](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)">挂起的 I/O 操作中 Postoperation 回调例程</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>同步操作</p></td>
<td align="left"><p>返回 FLT_PREOP_SYNCHRONIZE preoperation 回调例程。</p>
<p>请参阅<a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">返回 FLT_PREOP_SYNCHRONIZE</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>完成 preoperation 回调例程中的操作</p></td>
<td align="left"><p>设置的最后一个操作状态和中的信息<strong>IoStatus</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff544620" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544620)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作结构。</p>
<p>返回 FLT_PREOP_COMPLETE preoperation 回调例程。</p>
<p>请参阅<a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">完成 I/O 操作中 Preoperation 回调例程</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>完成操作后已 preoperation 回调例程中挂起</p></td>
<td align="left"><p>设置的最后一个操作状态和中的信息<strong>IoStatus</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff544620" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544620)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作结构。</p>
<p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff541913" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541913)"> <strong>FltCompletePendedPreOperation</strong> </a>从辅助线程处理 I/O 操作，将传递为 FLT_PREOP_COMPLETE <em>CallbackStatus</em>参数。</p>
<p>请参阅<a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">完成 I/O 操作中 Preoperation 回调例程</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>执行完成所有工作完成例程中</p></td>
<td align="left"><p>返回 FLT_POSTOP_FINISHED_PROCESSING postoperation 回调例程。</p>
<p>请参阅<a href="writing-postoperation-callback-routines.md" data-raw-source="[Writing Postoperation Callback Routines](writing-postoperation-callback-routines.md)">编写 Postoperation 回调例程</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不要在安全的 IRQL 完成工作</p></td>
<td align="left"><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff542047" data-raw-source="[&lt;strong&gt;FltDoCompletionProcessingWhenSafe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542047)"> <strong>FltDoCompletionProcessingWhenSafe</strong> </a> postoperation 回调例程。</p>
<p>请参阅<a href="ensuring-that-completion-processing-is-performed-at-safe-irql.md" data-raw-source="[Ensuring that Completion Processing is Performed at Safe IRQL](ensuring-that-completion-processing-is-performed-at-safe-irql.md)">确保安全的 IRQL 在执行完成处理</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>发出事件信号从完成例程</p></td>
<td align="left"><p>返回 FLT_PREOP_SYNCHRONIZE preoperation 回调例程对于此操作。</p>
<p>筛选器管理器在 preoperation 回调例程，在 IRQL 与相同的线程上下文中调用 postoperation 回调例程&lt;= APC_LEVEL。</p>
<p>请参阅<a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">返回 FLT_PREOP_SYNCHRONIZE</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>失败的成功创建操作</p></td>
<td align="left"><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff541784" data-raw-source="[&lt;strong&gt;FltCancelFileOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541784)"> <strong>FltCancelFileOpen</strong> </a>从创建操作的 postoperation 回调例程。</p>
<p>在中设置相应的错误 NTSTATUS 值<strong>IoStatus</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff544620" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544620)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作结构。</p>
<p>返回 FLT_POSTOP_FINISHED_PROCESSING。</p>
<p>请参阅<a href="failing-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Failing an I/O Operation in a Postoperation Callback Routine](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)">失败的 I/O 操作中 Postoperation 回调例程</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>禁止通过 I/O 操作的快速 I/O 路径 I/O</p></td>
<td align="left"><p>从操作 preoperation 回调例程返回 FLT_STATUS_DISALLOW_FAST_IO。</p>
<p>请参阅<a href="disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Disallowing a Fast I/O Operation in a Preoperation Callback Routine](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)">禁止 Preoperation 回调例程中的快速 I/O 操作</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>修改某个 I/O 操作的参数</p></td>
<td align="left"><p>在中设置已修改的参数值<strong>Iopb</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff544620" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544620)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作结构。</p>
<p>将 FLT_CALLBACK_DATA 结构标记为脏，通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544383" data-raw-source="[&lt;strong&gt;FltSetCallbackDataDirty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544383)"> <strong>FltSetCallbackDataDirty</strong></a>，除非修改的内容时<strong>IoStatus</strong> FLT_ 的成员CALLBACK_DATA 结构。</p>
<p>请参阅<a href="modifying-the-parameters-for-an-i-o-operation.md" data-raw-source="[Modifying the Parameters for an I/O Operation](modifying-the-parameters-for-an-i-o-operation.md)">修改为一个 I/O 操作的参数，</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>锁定用户缓冲区操作</p></td>
<td align="left"><p>使用的技术和中所述的指导原则<a href="accessing-the-user-buffers-for-an-i-o-operation.md" data-raw-source="[Accessing the User Buffers for an I/O Operation](accessing-the-user-buffers-for-an-i-o-operation.md)">I/O 操作中访问用户缓冲区</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 




