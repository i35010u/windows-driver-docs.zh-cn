---
title: 示例 DownloadPreviewImage
description: 示例 DownloadPreviewImage
ms.assetid: 9b27492e-0725-4c8b-9101-3aaf5c9291d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45cca254c5f64a723225c5fc5112f43a824803a1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192949"
---
# <a name="example-downloadpreviewimage"></a>示例： DownloadPreviewImage





**DownloadPreviewImage**函数通过调用预览组件的**IWiaPreview：： GetNewPreview**方法从扫描程序下载图像数据。 然后，如果应用程序用户想要调用分段筛选器，它将调用 **DetectSubregions** 函数，该功能会在其检测到的每个区域下的 *pWiaItem2* 下创建子项目。 有关此示例中使用的 **DetectSubregions**的信息，请参阅 [**IWiaSegmentationFilter：:D etectregions**](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiasegmentationfilter-detectregions) 方法。

在此示例中，应用程序用户通过单击复选框设置 *m \_ bUseSegmentationFilter* 参数。 如果应用程序支持此操作，它应该首先通过调用 **IWiaItem2：： CheckExtension**来检查驱动程序是否具有分段筛选器。 有关此示例中使用的 **CheckImgFilter**的信息，请参阅 Microsoft Windows SDK 文档中的 **IWiaPreview：： GetNewPreview** 方法。

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

 

