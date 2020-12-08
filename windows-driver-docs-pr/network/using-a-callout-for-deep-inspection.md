---
title: 使用标注进行深度检测
description: 使用标注进行深度检测
keywords:
- 分类标注 WDK Windows 筛选平台，深度检测
- 深度检查 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eba086e52114d5d42ad8fc41522e76d012673160
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806143"
---
# <a name="using-a-callout-for-deep-inspection"></a>使用标注进行深度检测


当标注执行深度检查时，它的 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) callout 函数可以检查固定数据字段、元数据字段以及传递给它的任何原始数据包数据的任意组合，以及与筛选器或数据流关联的上下文中存储的所有相关数据。

例如：

```C++
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
  PNET_BUFFER_LIST rawData;
  ...

  // Test for the FWPS_RIGHT_ACTION_WRITE flag to check the rights
  // for this callout to return an action. If this flag is not set,
  // a callout can still return a BLOCK action in order to VETO a
  // PERMIT action that was returned by a previous filter. In this
  // example the function just exits if the flag is not set.
 if (!(classifyOut->rights & FWPS_RIGHT_ACTION_WRITE))
  {
    // Return without specifying an action
 return;
  }

  // Get the data fields from inFixedValues
  ...

  // Get any metadata fields from inMetaValues
  ...

  // Get the pointer to the raw data
 rawData = (PNET_BUFFER_LIST)layerData;

  // Get any filter context data from filter->context
  ...

  // Get any flow context data from flowContext
  ...

  // Inspect the various data sources to determine
  // the action to be taken on the data
  ...

  // If the data should be permitted...
 if (...) {

    // Set the action to permit the data
 classifyOut->actionType = FWP_ACTION_PERMIT;

    // Check whether the FWPS_RIGHT_ACTION_WRITE flag should be cleared
 if (filter->flags & FWPS_FILTER_FLAG_CLEAR_ACTION_RIGHT)
    {
       // Clear the FWPS_RIGHT_ACTION_WRITE flag
 classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;
    }

 return;
  }

  ...

  // If the data should be blocked...
 if (...) {

    // Set the action to block the data
 classifyOut->actionType = FWP_ACTION_BLOCK;

    // Clear the FWPS_RIGHT_ACTION_WRITE flag
 classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;

 return;
  }

  ...

  // If the decision to permit or block should be passed
  // to the next filter in the filter engine...
 if (...) {

    // Set the action to continue with the next filter
 classifyOut->actionType = FWP_ACTION_CONTINUE;

 return;
  }

  ...
}
```

*Filter- &gt; action* 中的值可确定标注的 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) callout 函数应在 *ClassifyOut* 参数指向的结构的 **actionType** 成员中返回的操作。 有关这些操作的详细信息，请参阅 [**FWPS \_ ACTION0**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_action0) 结构。

如果标注必须先对其 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) callout 函数之外的数据包数据执行额外的处理，才能确定是应该允许还是阻止数据，则必须在完成数据处理之前挂起数据包数据。 有关如何挂起数据包数据的信息，请参阅 [标注类型](types-of-callouts.md) 和 [**FwpsPendOperation0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)。

在某些筛选层上，筛选器引擎传递给标注的 [classifyFn](/windows-hardware/drivers/ddi/_netvista/)标注函数的 *LayerData* 参数为 **NULL**。

有关如何对流数据执行深度检查的信息，请参阅 [使用标注对流数据进行深度检测](using-a-callout-for-deep-inspection-of-stream-data.md)。

 

