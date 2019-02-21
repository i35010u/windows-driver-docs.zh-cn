---
title: 示例默认分段的筛选器
description: 示例默认分段的筛选器
ms.assetid: 96c74ca6-0162-4991-b3f9-86c17c92ffc3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef65e94113e23644d31215a52f96f4d61e1e0f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540416"
---
# <a name="example-default-segmentation-filter"></a>示例：默认分段的筛选器


驱动程序不需要有自己分段的筛选器，以便充分利用 Microsoft 分段的筛选器，只要它实现了 WIA\_IP\_分段属性。 另一种可能性是 IHV 提供自己分段的筛选器，这在某些情况下调用到 Microsoft 默认 WIA 分段筛选。 例如，IHV 可能想要提供多区域检测期间扫描的电影胶片的非常特定于设备分段筛选器，并使用从平板扫描期间由 Microsoft 提供的分段筛选器。 若要执行此操作，IHV WIA 分段筛选器只需创建*CLSID\_WiaDefaultSegFilter*，它实现*IWiaSegmentationFilter;* 分段筛选器随后就可以调用*DetectRegions*。 下面的代码示例演示如何执行此操作。

```cpp
STDMETHODIMP
SegFilter::DetectRegions(
   IN LONG       lFlags,
     IN IStream    *pInputStream,
     IN IWiaItem2  *pWiaItem2)
{
    HRESULT  hr                = S_OK;
    GUID     categoryGUID      = {0};
    BOOL     bUseDefaultFilter = FALSE;

    ...


    if (SUCCEEDED(hr))

    {
        ReadPropertyLong(pWiaItem2,
                         WIA_IPA_ITEM_CATEGORY,
                         &categoryGUID);
 
        if (categoryGUID == WIA_CATEGORY_FILM)
        {
            bUseDefaultFilter = FALSE;
        }
        else if (categoryGUID == WIA_CATEGORY_FLATBED)
        {
            bUseDefaultFilter = TRUE;
        }
        else
        {
            //
            // This scanner only comes with flatbed and film items.
            //
            hr = E_INVALIDARG;
        }
    }
 
    ...
 
    if (SUCCEEDED(hr) && bUseDefaultFilter)
    {
        //
        // This must be on the flatbed item - use the Microsoft Default WIA Segmentation Filter.
        //

        IWiaSegmentationFilter *pDefaultSegFilter = NULL;
 
        hr = CoCreateInstance(CLSID_WiaDefaultSegFilter,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IWiaSegmentationFilter,
                              reinterpret_cast<void **>(&pDefaultSegFilter));
        if (SUCCEEDED(hr))
        {
            hr = pDefaultSegFilter->DetectRegions(lFlags, pInputStream, pWiaItem2);
        }
 
        if (pDefaultSegFilter)
        {
            pDefaultSegFilter->Release();
            pDefaultSegFilter = NULL;
        }
    }
    else if (SUCCEEDED(hr))
    {
        //
        // This is on the film item - use the default WIA segmentation algorithm.
        //
        ...
    }
    ...
}
```

 

 




