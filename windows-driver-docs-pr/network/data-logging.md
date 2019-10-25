---
title: 数据日志记录
description: 数据日志记录
ms.assetid: 1e4f00e0-0fc6-459d-bbdd-02fbca5b9945
keywords:
- 分类标注 WDK Windows 筛选平台，数据日志记录
- 记录 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e812754f21123d251e60ac382185399bc27a8ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834977"
---
# <a name="data-logging"></a>数据日志记录


若要确定应该记录哪些数据，标注的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/) callout 函数可以检查数据字段的任何组合、元数据字段以及传递给它的任何原始数据，以及存储在上下文中的任何相关数据与筛选器或数据流相关联。

例如，如果某一标注跟踪网络层中的某个筛选器丢弃多少个传入（入站） IPv4 数据包，则该标注将添加到 FWPM\_层的筛选器引擎\_入站\_IPPACKET\_V4\_放弃该层. 在这种情况下，标注的[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)标注函数可能类似于以下示例：

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


[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






