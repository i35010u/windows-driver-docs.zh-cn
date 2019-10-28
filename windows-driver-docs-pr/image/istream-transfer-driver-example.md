---
title: IStream 传输驱动程序示例
description: IStream 传输驱动程序示例
ms.assetid: fb830522-f95e-4dd7-8c1b-de092a6c5a51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c28170ac4c1d220d0aaa6b41a6ec308e598fda7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840803"
---
# <a name="istream-transfer-driver-example"></a>IStream 传输驱动程序示例


下面的代码示例演示了基于 IStream 的传输模型的实现。

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
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  



