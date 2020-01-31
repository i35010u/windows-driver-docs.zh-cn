---
title: 将上下文与数据流相关联
description: 将上下文与数据流相关联
ms.assetid: 75f5838e-626d-4a59-810e-fec9a40640ed
keywords:
- 分类标注 WDK Windows 筛选平台，与数据流相关联的上下文
- 上下文 WDK Windows 筛选平台
- flowContext 参数 WDK Windows 筛选平台
- 将上下文与数据流 WDK Windows 筛选平台相关联
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 59476e85f694924ef77aa5d3eb2475fa4ca08e63
ms.sourcegitcommit: 05c2f94fa2fe77276ca7000c1ff8e1bbe7a67b6a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2020
ms.locfileid: "76892192"
---
# <a name="associating-context-with-a-data-flow"></a>将上下文与数据流相关联


对于在支持数据流的筛选层处理数据的标注，标注驱动程序可以将上下文与每个数据流相关联。 此类上下文对于筛选器引擎是不透明的。 标注的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/) callout 函数可以使用此上下文保存特定于数据流的状态信息，以便下次由该数据流的筛选器引擎调用。 筛选器引擎通过*flowContext*参数将此上下文传递给标注的 classifyFn callout 函数。 如果没有上下文与数据流相关联，则*flowContext*参数为零。

若要将上下文与数据流相关联，标注的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/) callout 函数会调用[**FwpsFlowAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowassociatecontext0)函数。 例如：

```cpp
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  .
  .  // Driver-specific content
  .
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
  if (FWPS_IS_METADATA_FIELD_PRESENT(
      inMetaValues,
      FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
    flowHandle = inMetaValues->flowHandle;

    // Allocate the flow context structure
    context =
      (PFLOW_CONTEXT)ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(FLOW_CONTEXT),
        FLOW_CONTEXT_POOL_TAG
      );

    // Check the result of the memory allocation
    if (context == NULL) 
    {
 
      // Handle memory allocation error
      ...
    }
    else
    {

      // Initialize the flow context structure
      ...

      // Associate the flow context structure with the data flow
      status = FwpsFlowAssociateContext0(
                flowHandle,
                FWPS_LAYER_STREAM_V4,
                calloutId,
                (UINT64)context
              );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }
    }
  }

  ...

}
```

如果某个上下文已与数据流相关联，则必须先删除该上下文，然后才能将新的上下文与数据流相关联。 若要从数据流中删除上下文，标注的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/) callout 函数会调用[**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0)函数。 例如：

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
 if (FWPS_IS_METADATA_FIELD_PRESENT(
    inMetaValues,
    FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
     flowHandle = inMetaValues->flowHandle;

    // Check whether there is a context associated with the data flow
     if (flowHandle != 0) 
     {
        // Get a pointer to the flow context structure
        context = (PFLOW_CONTEXT)flowContext;

        // Remove the flow context structure from the data flow
        status = FwpsFlowRemoveContext0(
                  flowHandle,
                  FWPS_LAYER_STREAM_V4,
                  calloutId
                );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }

      // Cleanup the flow context structure
      ...

      // Free the memory for the flow context structure
      ExFreePoolWithTag(
        context,
        FLOW_CONTEXT_POOL_TAG
        );
    }
  }

  ...

}
```

在前面的示例中， *calloutId*变量包含标注的运行时标识符。 当标注驱动程序向筛选器引擎注册标注时，运行时标识符是返回给标注驱动程序的同一标识符。
