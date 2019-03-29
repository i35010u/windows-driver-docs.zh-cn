---
title: 使用标记进行对象引用跟踪
description: 使用标记进行对象引用跟踪
ms.assetid: f6c3d7b2-09b1-4055-b066-cce8831efab2
keywords:
- 使用 WDK 标记引用的对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92cd71cca13a7d87fb4e981215cef0f6c593964a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575897"
---
# <a name="object-reference-tracing-with-tags"></a>使用标记进行对象引用跟踪


[内核对象](managing-kernel-objects.md)是 Windows 内核实现在系统内存来表示由操作系统管理计算环境的各个部分中的基元数据对象。 内核对象表示功能，例如设备、 驱动程序、 文件、 注册表项、 事件、 信号量、 进程和线程。

大多数内核对象不是永久的。 若要防止非永久内核对象而内核模式驱动程序使用该对象中删除，该驱动程序可以获取对对象的计数的引用。 当驱动程序不再需要对象时，该驱动程序将释放其对该对象的引用。

如果驱动程序不会释放所有其引用的对象，该对象的引用计数永远不会减少为零并永远不会删除该对象。 因此，由对象 （例如，系统内存） 使用的系统资源都*泄漏*。 也就是说，它们不能使用在操作系统启动下一次之前。

如果驱动程序，会发生引用错误的另一种*下引用*对象。 在这种情况下，该驱动程序释放的对象的引用不是实际保存驱动程序。 此错误可能导致过早，其他客户端仍试图访问对象时删除的对象。

泄漏和未得到充分的内核对象的引用可能很困难 bug 来跟踪。 例如，将进程对象或一个设备对象可能具有数以万计的引用。 它可能很难识别在这些情况下的对象引用 bug 的源。

在 Windows 7 和更高版本的 Windows 中，可以标记对象的引用来轻松地找到这些 bug。 下面的例程标记相关联的获取和释放对内核对象的引用：

[**ObDereferenceObjectDeferDeleteWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff557732)

[**ObDereferenceObjectWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff557734)

[**ObReferenceObjectByHandleWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff558683)

[**ObReferenceObjectByPointerWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff558688)

[**ObReferenceObjectWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff558690)

例如， **ObReferenceObjectWithTag**并**ObDereferenceObjectWithTag**，可在 Windows 7 和更高版本的 Windows，是的增强的版本[ **ObReferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558678)并[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)例程，Windows 2000 和更高版本的 Windows 中可用。 这些增强的例程，可提供一个 4 字节的自定义标记值作为输入参数。 每次调用的标记值添加到[对象引用跟踪](https://go.microsoft.com/fwlink/p/?linkid=153590)可通过访问[Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=153599)。 **ObReferenceObject**并**ObDereferenceObject**执行不使调用方指定的自定义标记，但是，在 Windows 7 和更高版本的 Windows 中，这些例程 （具有标记值"Dflt"） 的默认标记添加到跟踪。 因此，调用**ObReferenceObject**或**ObDereferenceObject**具有相同的效果与调用**ObReferenceObjectWithTag**或**ObDereferenceObjectWithTag** ，它指定"Dflt"标记值。 （在程序中，此标记值表示为 0x746c6644 或 tlfD。）

若要跟踪的潜在对象泄漏或未得到充分的引用，标识一组相关联**ObReferenceObject*Xxx*WithTag**并**ObDereferenceObject*Xxx*WithTag**中您的驱动程序的递增和递减引用计数的特定对象的调用。 选择常见标记值 (例如，"Lky8") 使用此集中的所有调用。 您的驱动程序完成后使用对象的递减数应完全匹配增量的数。 如果这些编号不匹配，您的驱动程序已存在 bug，对象引用。 调试器可以递增和递减为每个标记值的数字进行比较，并告知您是否它们不匹配。 借助此功能，您可以快速找出源的引用计数不匹配。

若要在 Windows 调试工具中查看的对象引用跟踪，请使用[！ obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)内核模式调试程序扩展。 在 Windows 7 和更高版本的 Windows， [！ obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)扩展可以显示对象引用标记，如果启用了对象引用跟踪。 默认情况下，禁用对象引用跟踪。 使用[全局标志编辑器](https://go.microsoft.com/fwlink/p/?linkid=153601)(Gflags) 若要启用对象引用跟踪。 有关 Gflags 详细信息，请参阅[配置对象引用跟踪](https://go.microsoft.com/fwlink/p/?linkid=153602)。

启用了对象引用跟踪后，生成的输出[！ obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)扩展包括"标记"列中，如以下示例所示：

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

在此示例中的最后一行指示引用和取消引用与标记不匹配"Lky8"相关联的计数和一个 （也就是说，泄漏） 是过度引用的这种不匹配的结果。

如果结果已改为未得到充分的引用，最后一行[！ obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)输出可能如下所示：

```cpp
Tag: Lky8 References: 1 Dereferences: 2 Under reference by: 1
```

默认情况下，操作系统可以通过释放对象后删除对象的对象引用跟踪来节省内存。 若要跟踪未得到充分的引用，需要跟踪保留在内存中存储，甚至后释放该对象。 为此目的，Gflags 工具提供了"永久性"选项，该计算机关闭并重新启动时将保留在内存中的跟踪选项。

对象引用跟踪，不带标记，是在 Windows XP 中引入的。 因为跟踪不包含标记，开发人员必须使用不太方便技术来确定对象引用错误。 调试器无法跟踪组的开发人员选择的对象类型的对象的引用。 开发人员无法识别的对象引用的各种源和取消引用的唯一方法是比较其调用堆栈。 虽然以前[！ obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)示例包含只有五个堆栈，某些类型的对象，例如进程 ([**EPROCESS**](eprocess.md)) 对象，可能会引用和取消引用数以千计的次数。 具有数千个堆栈，以检查，可能难以识别对象泄漏或过少引用的源，而无需使用标记。
