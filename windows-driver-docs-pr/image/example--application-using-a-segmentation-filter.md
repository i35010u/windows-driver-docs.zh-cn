---
title: 示例应用程序使用分段的筛选器
description: 示例应用程序使用分段的筛选器
ms.assetid: 3f7de6a2-5684-4c37-97bc-47f4727114ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c706b9d7ee8ff3d33cdc5d60e765643586b4bb03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522293"
---
# <a name="example-application-using-a-segmentation-filter"></a>示例：应用程序使用分段的筛选器





下面的代码示例显示了一个简单的应用程序可以如何使用分段的筛选器。 为清楚起见，错误检查已省略代码，以及发布和免费的接口指针和内存的代码。

```cpp
IWiaSegmentationFilter *pWiaSegmentationFilter = NULL;
IWiaTransferCallback *pMyWiaTransferCallback = NULL;
IWiaTransfer  *pWiaTransfer = NULL;

...

pWiaItem2->QueryInterface(IID_IWiaTransfer, (void**)&pWiaTransfer);

pMyWiaTransferCallback = new MyWiaTransferCallback();


//
// Do preview scan.
//    
pWiaTransfer->Download(lFlags, pMyWiaTransferCallback);

//
// If an application changes any properties in pWiaItem2, it
// should call IWiaPropertyStorage::GetPropertyStream on
// that item to save its property settings (so they can be
// restored) before calling IWiaSegmentationFilter::DetectRegions.
//

if (ReadPropertyLong(WIA_IPS_SEGMENTATION_FILTER, &lUseSegFilter) &&
    (lUseSegFilter == WIA_USE_SEGMENTATION_FILTER)
{
    bstrSegmentation = SysAllocStr(WIA_SEGMENTATION_FILTER_STR);

    pWiaItem2->GetExtension(bstrSegmentation,
                            IID_IWiaSegmentationFilter,
                           (void**)& pWiaSegmentationFilter);

//
// m_pInputStream is a pointer to the IStream that the application's
// implementation of MyWiaTransferCallback::GetNextStream
// returns.
//
// Note: If the application has changed any properties into
// pWiaItem2 since the call to Download, it must now restore
// these properties with IWiaPropertyStorage::SetPropertyStream.
//

//
// The application is responsible for resetting m_pInputStream
// before calling DetectRegions!
//
    LARGE_INTEGER  ul = {0};

    m_pInputStream->Seek(ul, STREAM_SEEK_SET, NULL);

    pWiaSegmentationFilter->DetectRegions(m_pInputStream,
                                          pWiaItem2);

   ...
}

//
// Display the subregions to the users (if segmentation was
// supported) and let them pick the images they want to scan,
// as well as change the properties in the child items

//
// For each child item, pChildItem, do the following ( alternatively,
// do a folder acquisition on pWiaItem2).
//
IWiaTransfer  *pWiaTransferChild= NULL;

pChildItem->QueryInterface(IID_IWiaTransfer,
                           (void**)& pWiaTransferChild);

pWiaTransferChild->Download(lFlags, pMyWiaTransferCallback); 
```

 

 




