---
title: 使用标注进行深度检测
description: 使用标注进行深度检测
ms.assetid: 464c74ae-5e37-41f1-b305-ef57039b28ba
keywords:
- 分类标注 WDK Windows 筛选平台，深度检测
- 深度检测 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90398573152f2a067fcdd237243f97084cbd155a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369632"
---
# <a name="using-a-callout-for-deep-inspection"></a>使用标注进行深度检测


标注何时执行深度检测，其[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数可以检查固定的数据字段、 元数据字段和传递给它的任何原始数据包数据的任意组合，以及已被任何相关数据与筛选器或数据相关联的上下文中存储流。

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

中的值*筛选器-&gt;action.type*确定哪些操作的标注[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数应返回在**actionType**成员指向的结构*classifyOut*参数。 有关这些操作的详细信息，请参阅[ **FWPS\_ACTION0** ](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)结构。

如果一个标注必须执行其他处理外部的数据包数据及其[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数之前它可以确定是否应允许或阻止数据，它必须挂起数据包数据的处理之前完成数据。 有关如何挂起数据包数据的信息，请参阅[类型的标注](types-of-callouts.md)并[ **FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpspendoperation0)。

一些筛选层，*数据*参数，它由筛选器引擎传递到一个标注[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数是**NULL**。

有关如何执行深度检测数据进行流式传输的信息，请参阅[深度检测的 Stream 数据用于标注](using-a-callout-for-deep-inspection-of-stream-data.md)。

 

 





