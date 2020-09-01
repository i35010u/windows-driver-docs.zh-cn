---
title: 数据日志记录
description: 数据日志记录
ms.assetid: 1e4f00e0-0fc6-459d-bbdd-02fbca5b9945
keywords:
- 分类标注 WDK Windows 筛选平台，数据日志记录
- 记录 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f681c6f1e349d3602b6ef925f8c3c859f7796043
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218438"
---
# <a name="data-logging"></a>数据日志记录


若要确定应该记录哪些数据，标注的 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) callout 函数可以检查数据字段的任何组合、元数据字段以及传递给它的任何原始数据，以及与筛选器或数据流关联的上下文中存储的任何相关数据。

例如，如果某个标注跟踪网络层上的某个筛选器丢弃多少个传入 (入站) IPv4 数据包，则该标注将添加到 FWPM \_ 层 \_ 入站 \_ IPPACKET \_ V4 \_ 丢弃层上的筛选器引擎。 在这种情况下，标注的 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) 标注函数可能类似于以下示例：

```C++
ULONG TotalDiscardCount = 0;
ULONG FilterDiscardCount = 0;

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
  // Increment the total count of discarded packets
 InterlockedIncrement(&TotalDiscardCount);


  // Check whether a discard reason metadata field is present
 if (FWPS_IS_METADATA_FIELD_PRESENT(
 inMetaValues,
        FWPS_METADATA_FIELD_DISCARD_REASON))
  {
    // Check whether it is a general discard reason
 if (inMetaValues->discardMetadata.discardModule ==
        FWPS_DISCARD_MODULE_GENERAL)
    {
      // Check whether discarded by a filter
 if (inMetaValues->discardMetadata.discardReason ==
          FWPS_DISCARD_FIREWALL_POLICY)
      {
        // Increment the count of packets discarded by a filter
 InterlockedIncrement(&FilterDiscardCount);
      }
    }
  }

  // Take no action on the data
 classifyOut->actionType = FWP_ACTION_CONTINUE;
}
```

## <a name="related-topics"></a>相关主题


[classifyFn](/windows-hardware/drivers/ddi/_netvista/)

 

