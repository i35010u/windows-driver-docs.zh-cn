---
title: 示例默认分段筛选器
description: 示例默认分段筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe6ce1cff1faf4311a3b4de82c9b4571cdd50fbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816723"
---
# <a name="example-default-segmentation-filter"></a>示例：默认分段筛选器


驱动程序无需具有其自己的分段筛选器即可利用 Microsoft 分段筛选器，前提是它实现了 "WIA \_ ip \_ 分段" 属性。 一种可能的情况是 IHV 提供自己的分段筛选器，在某些情况下，它会调用 Microsoft 默认的 WIA 分段筛选器。 例如，在胶片扫描期间，IHV 可能需要为多区域检测提供一种非常特定于设备的分段筛选器，并使用由 Microsoft 提供的分段筛选器在平台中进行扫描。 为此，IHV WIA 分段筛选器只需创建用于实现 IWiaSegmentationFilter 的 *CLSID \_ WiaDefaultSegFilter* *;* 然后，分段筛选器将调用 *DetectRegions*。 下面的代码示例演示如何执行此操作。

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

 

 




