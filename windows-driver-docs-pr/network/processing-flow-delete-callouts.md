---
title: 处理流删除标注
description: 处理流删除标注
ms.assetid: e947b3b3-27c6-408f-aa02-6b20fa1b9748
keywords:
- Windows 筛选平台标注驱动程序 WDK，流删除标注
- 标注驱动程序 WDK Windows 筛选平台，流删除标注
- 流删除标注 WDK Windows 筛选平台
- flowDeleteFn
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc130d5246f663238fd1a65aa94811b1b190c159
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327651"
---
# <a name="processing-flow-delete-callouts"></a>处理流删除标注


当停止标注正在处理的数据流时，筛选器引擎会调用的标注[ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)标注函数如果标注驱动程序以前与数据关联上下文流。 一个标注*flowDeleteFn*标注函数执行任何必要清理之前停止数据流，则标注驱动程序与数据流相关联的上下文。

例如：

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// flowDeleteFn callout function
VOID NTAPI
 FlowDeleteFn(
    IN UINT16  layerId,
    IN UINT32  calloutId,
    IN UINT64  flowContext
    )
{
  PFLOW_CONTEXT context;

  // Get the flow context structure
 context = (PFLOW_CONTEXT)flowContext;

  // Cleanup the flow context structure
  ...

  // Free the memory for the flow context structure
 ExFreePoolWithTag(
 context,
    FLOW_CONTEXT_POOL_TAG
    );
}
```

筛选器引擎将自动删除时停止数据流，则一个标注与数据流相关联的上下文。 因此，一个标注不需要调用[ **FwpsFlowRemoveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551169)函数从其[ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)标注函数若要从数据流删除上下文。

 

 





