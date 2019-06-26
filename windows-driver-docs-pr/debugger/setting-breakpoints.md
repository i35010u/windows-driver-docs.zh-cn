---
title: 设置断点
description: 设置断点
ms.assetid: 9715c35a-0c8c-4e89-be28-2899f21ec964
keywords:
- 调试器引擎 API，设置断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 348b921af971f02cb4ab56d40dc9aaeb807ceb29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366393"
---
# <a name="setting-breakpoints"></a>设置断点


## <span id="ddk_using_breakpoints_dbx"></span><span id="DDK_USING_BREAKPOINTS_DBX"></span>


使用创建的断点[ **AddBreakpoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-addbreakpoint)方法。 此方法创建[IDebugBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugbreakpoint)对象，表示该断点。 它还设置*断点类型*（软件断点或处理器断点）。 一旦创建断点后，不能更改其类型。

与删除断点[**了 RemoveBreakpoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)方法。 这还会删除**IDebugBreakpoint**对象; 此对象不能再次使用。

**请注意**  虽然**IDebugBreakpoint**实现**IUnknown**接口方法**iunknown:: Addref**和**Iunknown:: Release**不用来控制该断点的生存期。 这些方法具有对该断点的生存期没有影响。 相反， **IDebugBreakpoint**的方法后删除对象[**了 RemoveBreakpoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)调用。

 

创建断点时，将为其给定一个唯一*断点 ID*。 此标识符不会更改。 但是，在删除该断点后，其 ID 可能用于另一个断点。 有关如何接收通知的删除断点的详细信息，请参阅[监视事件](monitoring-events.md)。

创建一个断点时，它最初处于禁用状态;这意味着它不会导致要停止执行的目标。 使用的方法可能会启用此断点[ **AddFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags)若要添加调试\_断点\_的 ENABLED 标志。

首先创建一个断点时，它具有 0x00000000 与之关联的内存位置。 可以通过更改该位置[ **SetOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffset)地址，或通过使用[ **SetOffsetExpression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffsetexpression)使用符号的表达式. 应从其初始值更改断点的位置，然后使用它。

 

 





