---
title: 使用标记进行对象引用跟踪
description: 使用标记进行对象引用跟踪
ms.assetid: f6c3d7b2-09b1-4055-b066-cce8831efab2
keywords:
- 用标记 WDK 引用对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c029697f5185f57858c992cef1008c4fb76b5db1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185138"
---
# <a name="object-reference-tracing-with-tags"></a>使用标记进行对象引用跟踪


[内核对象](managing-kernel-objects.md) 是 Windows 内核在系统内存中实现的基元数据对象，用来表示由操作系统管理的计算环境的各个部分。 内核对象表示设备、驱动程序、文件、注册表项、事件、信号量、进程和线程等功能。

大多数内核对象不是永久性的。 若要防止在内核模式驱动程序使用对象时删除永久内核对象，驱动程序可以获取对该对象的计数引用。 当驱动程序不再需要该对象时，驱动程序将释放其对对象的引用。

如果驱动程序没有释放对某个对象的所有引用，则该对象的引用计数从不减小到零，并且永远不会删除该对象。 因此，对象使用的系统资源 (例如，系统内存) *泄露*。 也就是说，在下次启动操作系统之前，不能使用它们。

如果下的驱动程序 *引用* 对象，则会发生另一种类型的引用错误。 在这种情况下，驱动程序比实际保存的对象更多引用对象。 此错误可能导致对象被过早删除，其他客户端仍在尝试访问该对象。

内核对象的泄漏和未引用的错误可能很难跟踪。 例如，进程对象或设备对象可能有数十个引用。 在这些情况下，很难确定对象引用 bug 的源。

在 windows 7 和更高版本的 Windows 中，可以对对象引用进行标记，使这些 bug 更易于查找。 以下例程将标记与对内核对象的引用的获取和释放相关联：

[**ObDereferenceObjectDeferDeleteWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobjectdeferdeletewithtag)

[**ObDereferenceObjectWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobjectwithtag)

[**ObReferenceObjectByHandleWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandlewithtag)

[**ObReferenceObjectByPointerWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointerwithtag)

[**ObReferenceObjectWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectwithtag)

例如，在 windows 7 和更高版本的 Windows 中可用的 **ObReferenceObjectWithTag** 和 **ObDereferenceObjectWithTag**是 [**ObReferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject) 和 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 例程的增强版本，这些版本在 windows 2000 和更高版本的 windows 中可用。 利用这些增强的例程，你可以提供一个四字节的自定义标记值作为输入参数。 每个调用的标记值都将添加到可由[Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=153599)访问的[对象引用跟踪](https://go.microsoft.com/fwlink/p/?linkid=153590)。 **ObReferenceObject** 和 **ObDereferenceObject** 不允许调用方指定自定义标记，但是，在 windows 7 和更高版本的 windows 中，这些例程将 (带有标记值 "Dflt" ) 添加到跟踪的默认标记。 因此，对 **ObReferenceObject** 或 **ObDereferenceObject** 的调用与指定标记值 "Dflt" 的 **ObReferenceObjectWithTag** 或 **ObDereferenceObjectWithTag** 的调用具有相同的效果。 在您的程序中 (，此标记值表示为0x746c6644 或 ' tlfD '。 ) 

若要跟踪潜在的对象泄漏或非引用请求，请在驱动程序中标识一组关联的 **ObReferenceObject*Xxx*WithTag** 和 **ObDereferenceObject*Xxx*WithTag** 调用，以便递增和递减特定对象的引用计数。 选择一个公共标记值 (例如 "Lky8" ) ，用于此集中的所有调用。 完成使用对象的驱动程序后，减量的数量应与完全匹配的增量数。 如果这些数字不匹配，则驱动程序将具有对象引用错误。 调试器可以比较每个标记值的递增量和减量，并告诉您它们是否不匹配。 利用此功能，你可以快速查明引用计数不匹配的源。

若要在 Windows 调试工具中查看对象引用跟踪，请使用 [！ obtrace](../debugger/-obtrace.md) 内核模式调试程序扩展。 在 windows 7 和更高版本的 Windows 中，如果启用了对象引用跟踪，则 [！ obtrace](../debugger/-obtrace.md) 扩展可以显示对象引用标记。 默认情况下，对象引用跟踪处于禁用状态。 使用 [全局标志编辑器](https://go.microsoft.com/fwlink/p/?linkid=153601) (Gflags) 启用对象引用跟踪。 有关 Gflags 的详细信息，请参阅 [配置对象引用跟踪](https://go.microsoft.com/fwlink/p/?linkid=153602)。

启用对象引用跟踪后，由 [！ obtrace](../debugger/-obtrace.md) 扩展生成的输出包含 "标记" 列，如以下示例所示：

```cpp
0: kd> !obtrace 0x8a226130
Object: 8a226130
 Image: leakyapp.exe
Sequence   (+/-)   Tag    Stack
--------   -----   ----   --------------------------------------------
      36    +1     Dflt      nt!ObCreateObject+1c4
                             nt!NtCreateEvent+93
                             nt!KiFastCallEntry+12a

      37    +1     Dflt      nt!ObpCreateHandle+1c1
                             nt!ObInsertObjectEx+d8
                             nt!ObInsertObject+1e
                             nt!NtCreateEvent+ba
                             nt!KiFastCallEntry+12a

      38    -1     Dflt      nt!ObfDereferenceObjectWithTag+22
                             nt!ObInsertObject+1e
                             nt!NtCreateEvent+ba
                             nt!KiFastCallEntry+12a

      39    +1     Lky8      nt!ObReferenceObjectByHandleWithTag+254
                             leakydrv!LeakyCtlDeviceControl+6c
                             nt!IofCallDriver+63
                             nt!IopSynchronousServiceTail+1f8
                             nt!IopXxxControlFile+6aa
                             nt!NtDeviceIoControlFile+2a
                             nt!KiFastCallEntry+12a

      3a    -1     Dflt      nt!ObfDereferenceObjectWithTag+22
                             nt!ObpCloseHandle+7f
                             nt!NtClose+4e
                             nt!KiFastCallEntry+12a
 
--------   -----   ----   --------------------------------------------
References: 3, Dereferences 2
Tag: Lky8 References: 1 Dereferences: 0 Over reference by: 1
```

此示例中的最后一行指示与 "Lky8" 标记相关联的引用和取消引用计数与 "" 标记不匹配，并且此不匹配的结果是一个 (的超引用，即) 泄露。

如果结果而不是一个引用，则 [！ obtrace](../debugger/-obtrace.md) 输出的最后一行可能如下所示：

```cpp
Tag: Lky8 References: 1 Dereferences: 2 Under reference by: 1
```

默认情况下，在释放对象后，操作系统通过删除对象的对象引用跟踪来节省内存。 若要向下跟踪下一个引用，则需要跟踪仍保留在内存中，即使在释放对象后也是如此。 为此，Gflags 工具提供了一个 "永久" 选项，该选项在计算机关闭并再次启动时将跟踪保存在内存中。

Windows XP 中引入了对象引用跟踪（无标记）。 由于跟踪未包含标记，因此开发人员必须使用不太方便的方法来识别对象引用错误。 调试器可以跟踪对象组的引用，开发人员根据对象类型选择这些引用。 开发人员识别对象引用和取消引用的各种源的唯一方法是比较它们的调用堆栈。 尽管 previous [！ obtrace](../debugger/-obtrace.md) 示例只包含五个堆栈，但某些类型的对象（例如进程 ([**EPROCESS**](eprocess.md)) 对象）可能会被引用并取消对数千次的取消引用。 使用上千个堆栈进行检查时，可能很难识别对象泄露源或不使用标记进行就地引用。