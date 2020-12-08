---
title: 示例 DetectSubregions
description: 示例 DetectSubregions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc33fcb5fb7c30143d121c63ab80bbf5fca150e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816721"
---
# <a name="example-detectsubregions"></a>示例： DetectSubregions





分段筛选器 *)  (传递* 到 **DetectSubregions** 方法中的流执行区域检测。 有关此示例中使用的 **CreateSegmentationFilter** 函数的信息，请参阅 Microsoft Windows SDK 文档中的 **IWiaItem2：： path.getextension 对** 方法。

```cpp
HRESULT
DetectSubregions(
   IN IStream   *pImageStream,
   IN IWiaItem2 *pWiaItem2)
{
   HRESULT                 hr                  = S_OK;
   IWiaSegmentationFilter* pSegmentationFilter = NULL;

   if (!pWiaItem2 || !pImageStream)
   {
      hr = E_INVALIDARG;
   }

   if (SUCCEEDED(hr))
   {
      hr = CreateSegmentationFilter(pWiaItem2, &pSegmentationFilter);
   }

   if (SUCCEEDED(hr))
   {
      hr = pSegmentationFilter->DetectRegions(pImageStream, pWiaItem2); 
   }

   if (pSegmentationFilter)
   {
      pSegmentationFilter->Release();
      pSegmentationFilter = NULL;
   }

   return hr;
}
```

 

 




