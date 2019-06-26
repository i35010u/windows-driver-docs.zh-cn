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
ms.openlocfilehash: 36fa9f32eacb042d91c44ff8578f8af89011fcc8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385474"
---
# <a name="processing-flow-delete-callouts"></a>处理流删除标注


当停止标注正在处理的数据流时，筛选器引擎会调用的标注[ *flowDeleteFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)标注函数如果标注驱动程序以前与数据关联上下文流。 一个标注*flowDeleteFn*标注函数执行任何必要清理之前停止数据流，则标注驱动程序与数据流相关联的上下文。

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

筛选器引擎将自动删除时停止数据流，则一个标注与数据流相关联的上下文。 因此，一个标注不需要调用[ **FwpsFlowRemoveContext0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowremovecontext0)函数从其[ *flowDeleteFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)标注函数若要从数据流删除上下文。

 

 





