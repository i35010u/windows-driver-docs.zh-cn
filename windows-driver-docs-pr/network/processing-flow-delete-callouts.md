---
title: 处理流删除标注
description: 处理流删除标注
keywords:
- Windows 筛选平台标注驱动程序 WDK，流删除标注
- 标注驱动程序 WDK Windows 筛选平台，流删除标注
- 流删除标注 WDK Windows 筛选平台
- flowDeleteFn
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c65b790b7b0bf33cc213dd66b6726781392a234
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822843"
---
# <a name="processing-flow-delete-callouts"></a>处理流删除标注


当标注正在处理的数据流停止时，如果标注驱动程序以前将上下文与数据流相关联，则筛选器引擎将调用标注的 [*flowDeleteFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0) 标注函数。 标注的 *flowDeleteFn* callout 函数在数据流停止之前，对标注驱动程序与数据流相关联的上下文执行任何必要的清理。

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

当数据流停止时，筛选器引擎会自动删除与数据流关联的标注的上下文。 因此，在从数据流中删除上下文的 [**FwpsFlowRemoveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0)函数时，不 [*flowDeleteFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)需要使用标注。

 

