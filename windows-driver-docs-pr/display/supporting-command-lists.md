---
title: 支持命令列表
description: 支持命令列表
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，命令列表
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，命令列表
- 命令列表支持 WDK Windows 7 显示
- 命令列表支持 WDK Windows 7 显示，Direct3D 版本11
- 命令列表支持 WDK Windows 2008 R2 显示
- 命令列表支持 WDK Windows 2008 R2 显示，Direct3D 版本11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c483b3d2fded654f7dfbe0dffab51600c7d94ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831539"
---
# <a name="supporting-command-lists"></a>支持命令列表


本部分仅适用于 Windows 7 和更高版本以及 Windows Server 2008 R2 及更高版本的 Windows。

Direct3D 运行时使用以下适用于命令列表的 Direct3D 11 DDI：

-   [**CalcPrivateCommandListSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatecommandlistsize)函数确定命令列表的用户模式显示驱动程序的专用内存区域大小。

-   [**CreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)函数创建命令列表。

-   [**RecycleCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)函数将回收命令列表。

-   [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)函数创建命令列表，并使以前未使用的 DDI 句柄再次失效。

-   [**DestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)函数销毁命令列表。

-   [**RecycleDestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)函数通知驱动程序需要对命令列表进行轻型销毁。

-   [**CommandListExecute**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)函数运行命令列表。

驱动程序的 [**CommandListExecute**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)、 [**CalcPrivateCommandListSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatecommandlistsize)、 [**CreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)和 [**DestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist) 函数的语义大多都可以根据其他类似的 ddi 函数和相应 ddi 的 API 文档进行自我说明。

当 Direct3D 运行时在 *CreateCommandList* 参数指向的 [**D3D11DDIARG \_ pCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createcommandlist)结构的 **hDeferredContext** 成员中指定的延迟上下文上成功调用驱动程序的 [**CreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)或 [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)函数后，direct3d 运行时将在延迟的上下文中执行以下析构序列：

1.  Direct3D 运行时 "关闭" 所有打开的延迟对象句柄。 请注意，这些句柄可能仍会绑定到延迟的上下文。

2.  运行时销毁延迟的上下文。

在对 [**CreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist) 或 [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)的调用期间，驱动程序对 [状态刷新 DDI 回调函数](/windows-hardware/drivers/ddi/index) 所做的任何调用都将继续愿意延迟上下文的当前状态。 但是，在延迟上下文的 "正在关闭" 和 "销毁" 过程中，对状态刷新 DDI 的任何调用都将反映未绑定任何内容 (也就是说，在调用 *CreateCommandList* 或 *RecycleCreateCommandList* 后，所有内容都将隐式取消绑定) 。

延迟的上下文也可由应用程序显式放弃，或因 API 或驱动程序的错误条件而放弃。 对于这种情况，Direct3D 运行时将执行以下序列：

1.  Direct3D 运行时调用驱动程序的 [**AbandonCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist) 函数。

2.  运行时逐个解除对延迟上下文的句柄。

3.  运行时 "关闭" 所有打开的延迟对象句柄。

4.  运行时 recyles 或销毁延迟的上下文。

上述序列类似于直接上下文的析构序列。 对驱动程序的 [**AbandonCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_abandoncommandlist) 函数的调用为驱动程序提供了一种机会，使其能够将状态应用到驱动程序首选的任何内容。

在对驱动程序的 [**CommandListExecute**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute) 函数的调用过程中，驱动程序必须转换延迟上下文的状态，使其与创建设备时的状态等效。 此操作也称为 "清除状态" 操作。 但是，在调用驱动程序的 **CommandListExecute** 函数时，驱动程序对 [状态刷新 DDI 回叫函数](/windows-hardware/drivers/ddi/index) 所做的任何调用仍将反映在对驱动程序函数的上一次 DDI 调用期间绑定的内容的状态。 在下一次 DDI 调用驱动程序函数的过程中，驱动程序对状态刷新 DDI 回调函数所做的任何调用都将当前状态显示为完全为空，这反映了从 **CommandListExecute** 隐式的状态转换。 此事实与状态刷新 DDI 回叫函数的典型语义和行为稍有不同。 如果在对某个驱动程序的 *SetShader* 函数的调用过程中，驱动程序已调用状态刷新 ddi 回叫函数，则状态刷新 DDI 回叫函数将显示为已绑定的新着色器。 状态刷新 DDI 回叫行为的这种分歧为驱动程序提供了更大的灵活性，以便在 **CommandListExecute** 期间反映旧状态。

Direct3D 版本 11 API 确保未对任何查询都进行处理 (即，通过命令列表) 调用了 [**QueryBegin**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querybegin) 或 [**QueryEnd**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_queryend) ，并且仅由尝试执行命令列表的上下文 "开始"。 该 API 还可以确保不会在当前映射了相同资源的上下文中执行记录动态资源映射的命令列表。 在应用程序调用 **FinishCommandList** 函数之前，Direct3D 运行时对仍保留已开始的查询或已映射资源的任何查询或动态资源调用驱动程序的 **QueryEnd** 和 [**ResourceUnmap**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap) DDI 函数，因为 **FinishCommandList** 隐式终止查询范围并 messagebox 取消任何映射的资源。

### <a name="span-idoptimization_for_small_command_listsspanspan-idoptimization_for_small_command_listsspan-optimization-for-small-command-lists"></a><span id="optimization_for_small_command_lists"></span><span id="OPTIMIZATION_FOR_SMALL_COMMAND_LISTS"></span> 优化小命令列表

对于小内存量的命令列表，内存回收优化对于减少命令列表 DDI 函数调用中的争用和减少命令列表所需的调用处理的开销可能很重要。 每个命令列表中 inherant 的处理开销都非常重要。 此优化适用于命令列表，其中，命令列表所需的处理开销支配命令列表所需的 CPU 时间和内存空间。 例如，一个小内存量的命令列表，如 CopyResource。 CopyResource 所需的内存量为两个指针。 但是，CopyResource 仍要求使用与大内存量命令列表相同的命令列表调用处理量。 如果以高频率生成小内存量命令列表，则运行时调用驱动程序的 [**CreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcommandlist)、 [**DestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)、 [**CreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)和 [**DestroyDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroydevice) 函数 () 的处理开销会变得越来越重要。 此处引用的内存是包含驱动程序数据结构的系统内存，其中包括 DDI 句柄的内存。

驱动程序的 [**RecycleCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist) 函数必须通知驱动程序 (，驱动程序句柄不会使用，但尚未) 删除，并且在以前未使用的驱动程序句柄被重新使用时。 此通知适用于命令列表和延迟上下文句柄。 驱动程序必须回收的唯一内存是 DDI 句柄指向的内存。 尽管 **RecycleCommandList** 的目标是回收与句柄关联的内存，但为了提高效率，驱动程序可以灵活地选择和选择要回收的内存。 驱动程序无法更改直接上下文命令列表处理点的内存区域的大小。 此大小是 [**CalcPrivateCommandListSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatecommandlistsize)的返回值。 驱动程序还无法更改上下文命令列出本地句柄的内存区域的大小。此大小是 [**CalcDeferredContextHandleSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)的返回值。

驱动程序的 [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist) 和 [**RecycleCreateDeferredContext**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatedeferredcontext) DDI 函数必须将内存不足错误代码作为 E \_ OUTOFMEMORY HRESULT 值返回。 这些函数不会通过调用 [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) 函数提供此类错误代码。 此驱动程序要求会使运行时不必使用设备范围的同步来监视这些 create 类型驱动程序函数的即时上下文错误。 监视这些错误会成为小内存量命令列表的灾难性争用源。

驱动程序的 [**RecycleDestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)、 [**RecycleCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)和 [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist) 函数之间的区别很重要。 其功能包括：

<span id="RecycleDestroyCommandList"></span><span id="recycledestroycommandlist"></span><span id="RECYCLEDESTROYCOMMANDLIST"></span>[**RecycleDestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist)  
运行时调用驱动程序的 [**RecycleDestroyCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroycommandlist) 函数，以通知驱动程序需要轻型销毁。 也就是说，驱动程序不应为 DDI 命令列表句柄释放内存。 驱动程序的 *RecycleDestroyCommandList* 函数是自由线程，就像驱动程序的 **DestroyCommandList** 函数一样。

<span id="RecycleCommandList"></span><span id="recyclecommandlist"></span><span id="RECYCLECOMMANDLIST"></span>[**RecycleCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist)  
驱动程序的 [**RecycleCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecommandlist) 函数通知驱动程序运行时将命令列表句柄集成回延迟的上下文缓存。 然后，该函数为驱动程序提供了一种机会，以便将与命令列表关联的内存集成回延迟上下文缓存。 运行时通过延迟上下文线程调用驱动程序的 **RecycleCommandList** 函数。 **RecycleCommandList** DDI 函数降低了驱动程序执行其自身同步的需要。

<span id="RecycleCreateCommandList"></span><span id="recyclecreatecommandlist"></span><span id="RECYCLECREATECOMMANDLIST"></span>[**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist)  
运行时调用驱动程序的 [**RecycleCreateCommandList**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_recyclecreatecommandlist) 函数，使以前未使用的 DDI 句柄再次生效。

这些回收 DDI 函数提供优化机会，有助于回收小内存量命令列表的资源。 下面的伪代码演示了如何通过从 API 到 DDI 的函数调用流实现运行时：

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

以下状态图显示了即时上下文 DDI 命令列表句柄的有效性。 绿色状态表示可与 [**CommandListExecute**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)一起使用的句柄。

![说明命令列表句柄有效性状态的关系图](images/d3d11ddi2.png)

 

