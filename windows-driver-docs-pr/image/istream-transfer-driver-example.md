---
title: IStream 传输驱动程序示例
description: IStream 传输驱动程序示例
ms.assetid: fb830522-f95e-4dd7-8c1b-de092a6c5a51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0697602df3a66d0c1e538686705684d0306656b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378899"
---
# <a name="istream-transfer-driver-example"></a>IStream 传输驱动程序示例


下面的代码示例显示了基于 IStream 传输模型的实现。

```cpp
MyWiaDriver::drvAcquireItemData(
BYTE                      *pWiasContext,
LONG                      lFlags,
PMINIDRV_TRANSFER_CONTEXT pmdtc,
LONG                      *plDevErrVal)
{
   // Check what kind of data transfer is requested.
   if (lFlags & WIA_MINIDRV_TRANSFER_DOWNLOAD)
   {
      // This transfer is a stream-based download.
      IWiaMiniDrvTransferCallback *pTransferCallback = NULL;
      hr = pmdtc->pIWiaMiniDrvCallBack->QueryInterface(IID_IWiaMiniDrvTransferCallback,
             (void**) &pIWiaMiniDrvTransferCallback);
      if (SUCCEEDED(hr))
      {
         IStream *pDestination = NULL;
         // Get the destination stream from the client.
         hr = pTransferCallback->GetNextStream(0, 
                                               bstrItemName,
                                               bstrFullItemName,
                                               &pDestination);
         if (hr == S_OK)
         {
            BYTE    *pBuffer = ...
            ULONG   ulBytesRead = 0;
            // Read the next chunk of data into the buffer.
            while(GetNextDataBand(pBuffer, &ulBytesRead))
            {
               // Write the data to the destination stream.
               // The driver does not need to know what the
               // destination is.
               hr = pDestination->Write(...);

               if (SUCCEEDED(hr))
               {
                  // Send progress
                  hr = pTransferCallback->SendMessage(...)
               }

               else
               {
                  // Take appropriate error action (for example, abort transfer)
               }

            }
         }
      }
   .
   .
   .
   }
}
```

## <a name="related-topics"></a>相关主题
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  



