---
title: 支持命令列表
description: 支持命令列表
ms.assetid: 7bede247-680d-4fd3-a10b-6ef63f0a88ec
keywords:
- Direct3D 11 版 WDK Windows 7 显示，命令将列出
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，命令将列出
- 命令将列出支持 WDK Windows 7 显示
- 命令将列出支持 WDK Windows 7 显示，Direct3D 版本 11
- 命令列表支持 WDK Windows 2008 R2 显示
- 命令列表支持 WDK Windows 2008 R2 显示，Direct3D 版本 11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f5af08f8007d15b2dfe477def41abcf4864fc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566924"
---
# <a name="supporting-command-lists"></a>支持命令列表


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows。

Direct3D 运行时使用以下 Direct3D 11 DDI 的命令列表：

-   [ **CalcPrivateCommandListSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538278)函数将确定用户模式显示驱动程序的专用区域的命令列表的内存的大小。

-   [ **CreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff540602)函数会创建命令列表。

-   [ **RecycleCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569237)函数回收命令列表。

-   [ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)函数创建命令列表，并使以前未使用的 DDI 句柄再次完全有效。

-   [ **DestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)函数会销毁命令列表。

-   [ **RecycleDestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)函数会通知驱动程序的命令列表的轻量析构是必需。

-   [ **CommandListExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff539476)函数运行的命令列表。

驱动程序的语义[ **CommandListExecute**](https://msdn.microsoft.com/library/windows/hardware/ff539476)， [ **CalcPrivateCommandListSize**](https://msdn.microsoft.com/library/windows/hardware/ff538278)， [ **CreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff540602)，并[ **DestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)函数主要是自我解释，根据其他类似 DDI 函数和 API相应 DDI 的文档。

在 Direct3D 后运行时已成功调用的驱动程序[ **CreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff540602)或[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)函数延迟中指定的上下文**hDeferredContext**的成员[ **D3D11DDIARG\_CREATECOMMANDLIST** ](https://msdn.microsoft.com/library/windows/hardware/ff542040)结构*pCreateCommandList*参数所指向，Direct3D 运行时上下文中执行以下析构序列延迟：

1.  Direct3D 运行时"关闭"所有打开的延迟的对象句柄。 请注意，这些句柄可能仍会显示绑定到推迟的上下文。

2.  在运行时销毁推迟的上下文。

在调用[ **CreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff540602)或[ **RecycleCreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569238)，驱动程序对任何调用[状态刷新 DDI 回调函数](https://msdn.microsoft.com/library/windows/hardware/ff552885)继续将泄露推迟的上下文的当前状态。 但是，在"正在关闭"和析构的推迟的上下文，对状态刷新 DDI 的任何调用反映绑定执行任何操作 (即，在调用后立即*CreateCommandList*或*RecycleCreateCommandList*，所有内容都是隐式绑定)。

推迟的上下文可以还放弃显式由应用程序或由于错误条件而通过 API 或驱动程序。 对于这种情况下，Direct3D 运行时执行以下顺序：

1.  Direct3D 运行时调用的驱动程序[ **AbandonCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff538199)函数。

2.  在运行时取消绑定一个一个地推迟的上下文中的句柄。

3.  在运行时"关闭"所有打开的延迟的对象句柄。

4.  在运行时任一 recyles 或销毁推迟的上下文。

上述顺序是类似于即时上下文析构序列。 对驱动程序的调用[ **AbandonCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff538199)函数提供了驱动程序将状态应用到任何驱动程序首选的机会。

在驱动程序在调用[ **CommandListExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff539476)函数，该驱动程序必须转换推迟的上下文，以使其等效于状态创建设备时的状态。 此操作也称为是清除状态操作。 在驱动程序在调用**CommandListExecute**函数，但是，该驱动程序对任何调用[状态刷新 DDI 回调函数](https://msdn.microsoft.com/library/windows/hardware/ff552885)仍反映什么绑定期间的状态最后一个 DDI 调用驱动程序函数。 在驱动程序函数的后续 DDI 调用，任何驱动程序对状态刷新 DDI 回调函数的调用会显示当前状态为完全为空，这反映了隐式从状态转换**CommandListExecute**. 这一事实从典型语义和状态刷新 DDI 回调函数的行为略有不同。 如果该驱动程序已在一个驱动程序的调用期间调用状态刷新 DDI 回调函数*SetShader*函数，该状态刷新 DDI 回调函数将显示为已绑定被绑定的新着色器。 此分歧状态刷新 DDI 回调行为提供了驱动程序，以反映过程的旧状态可以更加灵活**CommandListExecute**。

Direct3D 11 版 API 可确保，没有查询已被同时操作 (即，具有[ **QueryBegin** ](https://msdn.microsoft.com/library/windows/hardware/ff569214)或[ **QueryEnd** ](https://msdn.microsoft.com/library/windows/hardware/ff569217)对其进行调用) 的命令列表和已仅"开始"的尝试执行命令列表的上下文。 API 还可确保具有相同的资源当前映射的上下文执行没有记录的映射的动态资源的命令列表。 应用程序调用之前**FinishCommandList**函数，Direct3D 运行时调用的驱动程序**QueryEnd**并[ **ResourceUnmap** ](https://msdn.microsoft.com/library/windows/hardware/ff569495)在任何查询或动态资源仍保留开始查询或映射的资源上 DDI 函数打开，因为**FinishCommandList**隐式终止查询范围，并取消映射映射的任何资源。

### <a name="span-idoptimizationforsmallcommandlistsspanspan-idoptimizationforsmallcommandlistsspan-optimization-for-small-command-lists"></a><span id="optimization_for_small_command_lists"></span><span id="OPTIMIZATION_FOR_SMALL_COMMAND_LISTS"></span> 优化的小命令列表

小内存量命令列表的优化的内存回收可以减少命令列表 DDI 函数调用间的争用以及以减少所需的命令列表的调用处理的开销很重要。 Inherant 每个命令列表中的处理开销很重要。 这种优化适用于其中的处理开销所需的命令列表支配的 CPU 时间和内存空间所需的命令列表的命令列表。 例如，小内存量命令列表是单个图形命令，如 CopyResource。 CopyResource 两个指针所需的内存量。 但是，CopyResource 仍需要处理作为较大内存量命令列表的命令列表调用相同的量。 高频率生成小内存量命令列表时, 的处理开销调用所需的运行时，驱动程序的[ **CreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff540602)， [ **DestroyCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff552748)， [ **CreateDeferredContext**](https://msdn.microsoft.com/library/windows/hardware/ff540622)，并[ **DestroyDevice(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff552768)函数 （对于延迟上下文） 变得日益重要。 此处提到的内存是保存驱动程序的数据结构，其中包括 DDI 句柄的内存的系统内存。

在驱动程序[ **RecycleCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569237)函数必须通知该驱动程序时驱动程序句柄进入扩展的使用 （但不是会删除），以及何时以前未使用的驱动程序句柄是重复使用。 此通知将应用到命令列表和延迟的上下文句柄。 该驱动程序必须回收的唯一内存是 DDI 处理指向的内存。 尽管的目的**RecycleCommandList**是效率驱动程序有很灵活地选择哪些内存回收回收句柄，与关联的内存。 该驱动程序不能更改的即时上下文命令列表到处理点的内存区域的大小。 此大小是返回的值[ **CalcPrivateCommandListSize**](https://msdn.microsoft.com/library/windows/hardware/ff538278)。 该驱动程序也不能更改的所属上下文命令列表本地处理点的内存区域的大小。此大小是返回的值[ **CalcDeferredContextHandleSize**](https://msdn.microsoft.com/library/windows/hardware/ff538272)。

在驱动程序[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)并[ **RecycleCreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff569239) DDI 函数必须返回内存不足错误代码为 E\_OUTOFMEMORY HRESULT 值。 这些函数不提供通过调用此类错误代码[ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)函数。 此驱动程序要求可防止在运行时无需使用设备级同步要监视的即时上下文错误从这些创建类型驱动程序函数。 观看这些错误会发生灾难性争用小内存量命令列表的源。

在驱动程序的之间的区别[ **RecycleDestroyCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff552748)， [ **RecycleCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569237)，和[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)函数也很重要。 其功能包括：

<span id="RecycleDestroyCommandList"></span><span id="recycledestroycommandlist"></span><span id="RECYCLEDESTROYCOMMANDLIST"></span>[**RecycleDestroyCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff552748)  
运行时调用的驱动程序[ **RecycleDestroyCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff552748)函数，以通知轻型析构是必需的驱动程序。 也就是说，驱动程序不应尚未取消分配内存 DDI 命令列表句柄。 在驱动程序*RecycleDestroyCommandList*函数是自由线程就像在驱动程序一样**DestroyCommandList**函数。

<span id="RecycleCommandList"></span><span id="recyclecommandlist"></span><span id="RECYCLECOMMANDLIST"></span>[**RecycleCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569237)  
在驱动程序[ **RecycleCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569237)函数告知驱动程序运行时集成回延迟的上下文缓存的命令列表句柄。 该函数然后提供有机会将与命令列表返回到延迟的上下文缓存相关联的内存进行驱动程序。 运行时调用的驱动程序**RecycleCommandList**从延迟的上下文线程的函数。 **RecycleCommandList** DDI 函数降低了驱动程序来执行其自己的同步。

<span id="RecycleCreateCommandList"></span><span id="recyclecreatecommandlist"></span><span id="RECYCLECREATECOMMANDLIST"></span>[**RecycleCreateCommandList**](https://msdn.microsoft.com/library/windows/hardware/ff569238)  
运行时调用的驱动程序[ **RecycleCreateCommandList** ](https://msdn.microsoft.com/library/windows/hardware/ff569238)函数可再次完全有效以前未使用的 DDI 句柄。

这些循环使用 DDI 函数提供优化机会，帮助回收小内存量命令列表的资源。 下面的伪代码显示了运行时通过从 API 到 DDI 的函数调用的流的实现：

```cpp
::FinishCommandList()
{
  // Empty InterlockedSList, integrating into the cache
  Loop { DC::pfnRecycleCommandList }

  If (Previously Destroyed CommandList Available)
 { IC::pfnRecycleCreateCommandList }
 else
  {
    IC::pfnCalcPrivateCommandListSize
    IC::pfnCreateCommandList
    IC::pfnCalcDeferredContextHandleSize(D3D11DDI_HT_COMMANDLIST)
  }

  Loop { DC::pfnDestroy* (context-local handle destroy) }

  IC::pfnRecycleCreateDeferredContext
}
...
Sporadic: DC::pfnCreate* (context-local open during first-bind per CommandList)

CommandList::Destroy()
{
  // If DC still alive, almost always recycle:
  If (DC still alive)
 { IC::pfnRecycleDestroyCommandList }
  Else
 { IC::pfnDestroyCommandList }
  // Add to InterlockedSList
}
```

以下状态图显示了即时上下文 DDI 命令列表句柄的有效性。 绿色状态表示可用于的句柄[ **CommandListExecute**](https://msdn.microsoft.com/library/windows/hardware/ff539476)。

![说明命令列表句柄有效性状态关系图](images/d3d11ddi2.png)

 

 





