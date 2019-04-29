---
title: 示例 DownloadPreviewImage
description: 示例 DownloadPreviewImage
ms.assetid: 9b27492e-0725-4c8b-9101-3aaf5c9291d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8387296f39b26a4d7c71d84c0a4fbef8ee0db75e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373101"
---
# <a name="example-downloadpreviewimage"></a>例如：DownloadPreviewImage





**DownloadPreviewImage**函数通过调用预览组件的扫描程序从下载图像数据**IWiaPreview::GetNewPreview**方法。 然后，它调用**DetectSubregions**函数，如果应用程序用户想要调用分段的筛选器，这将创建下的子项*pWiaItem2*为检测到每个区域。 璝惠**DetectSubregions**，用于在此示例中，请参阅[ **IWiaSegmentationFilter::DetectRegions** ](https://msdn.microsoft.com/library/windows/hardware/ff545030)方法。

在此示例中，应用程序用户设置*m\_bUseSegmentationFilter*参数通过单击复选框。 如果应用程序支持此功能，它应首先检查驱动程序通过调用已分段的筛选器**IWiaItem2::CheckExtension**。 璝惠**CheckImgFilter**，用于在此示例中，请参阅**IWiaPreview::GetNewPreview** Microsoft Windows SDK 文档中的方法。

```cpp
HRESULT
DownloadPreviewImage(
  IN IWiaItem2 *pWiaFlatbedItem2)
{
  HRESULT              hr = S_OK;
  BOOL                 bHasImgFilter  = FALSE;
  IWiaTransferCallback *pAppWiaTransferCallback = NULL;

  hr = CheckImgFilter(pWiaFlatbedItem2, &bHasImgFilter)

  if (SUCCEEDED(hr))
  {
     if (bHasImgFilter)
     {
        IWiaPreview *pWiaPreview = NULL;

        // In this example, the AppWiaTransferCallback class 
        // implements the IWiaTransferCallback interface.
         // The constructor of AppWiaTransferCallback sets the 
         // reference count to 1.
         pAppWiaTransferCallback = new AppWiaTransferCallback();

         hr = pAppWiaTransferCallback ? S_OK : E_OUTOFMEMORY;

         if (SUCCEEDED(hr))
         {
            // Acquire image from scanner
            hr = m_pWiaPreview->GetNewPreview(pWiaFlatbedItem2,
                                              0,
                                              pAppWiaTransferCallback);    
         }

         // m_FlatbedPreviewStream is the stream that
         // AppWiaTransferCallback::GetNextStream returned for the
         // flatbed item.
         // This stream is where the image data is stored after
         // the successful return of GetNewPreview.
         // The stream is passed into the segmentation filter
         // for region detection.
         if (SUCCEEDED(hr) && m_bUseSegmentationFilter)
         {
            DetectSubregions(m_FlatbedPreviewStream, pWiaFlatbedItem2);
         }

         if (pAppWiaTransferCallback)
         {
            // If the call to GetNewPreview was successful, the
            // preview component calls AddRef on the callback so
            // this call doesn't delete the object.

            pAppWiaTransferCallback->Release();
         }

      }
      else
      {
         // Do not create an instance of preview component if the 
         // driver does not come with an image-processing filter.
         // You can use a segmentation filter, however, if the driver
         // comes with one (omitted here).
      }
   }

   return hr;
}
```

 

 




