---
title: ESC_TWAIN_PRIVATE_SUPPORTED_CAPS 转义码
description: ESC_TWAIN_PRIVATE_SUPPORTED_CAPS 转义码
ms.assetid: 99b9f180-018b-47c4-ab8d-dc037e3f637a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6154d1798b948f11cc4fac5e58f0f03036a101f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192959"
---
# <a name="esc_twain_private_supported_caps-escape-code"></a>ESC \_ TWAIN \_ 私有 \_ 支持的 \_ 大写转义代码





为了确定支持 TWAIN 的私有功能，TWAIN 应用程序将通知 TWAIN 兼容层，后者随后将 ESC \_ TWAIN \_ 支持的 \_ \_ 大写转义代码发送到 WIA 驱动程序的 [**IStiUSD：： escape**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape) 方法。 以下 **转义** 方法的伪代码实现演示了如何响应 ESC \_ twain \_ 私有 \_ 支持的 \_ 大写转义代码，以报告私有 TWAIN 支持功能。

**注意**   在此示例中， **Escape**方法与[ESC \_ TWAIN \_ 功能转义代码](esc-twain-capability-escape-code.md)中所示的方法相同，但每个示例的焦点都是不同的转义码。

 

```cpp
STDMETHODIMP CWIADevice::Escape(STI_RAW_CONTROL_CODE EscapeFunction,
  LPVOID               lpInData,
  DWORD                cbInDataSize,
  LPVOID               pOutData,
  DWORD                dwOutDataSize,
  LPDWORD              pdwActualData)
{
  //
  // Only process EscapeFunction codes that are known to your driver.
  // Any application can send escape calls to your driver using the
  // IWiaItemExtras interface Escape() method call.  The driver must
  // be prepared to validate all incoming calls to Escape().
  //

  //
  // Because this driver does not support any escape functions, it will
  // reject all incoming EscapeFunction codes.
  //
  // If your driver supports an EscapeFunction, then add your function
  // code to the switch statement, and set hr = S_OK. This will allow
  // the function to continue to the incoming/outgoing buffer
  // validation.
  //

  HRESULT hr = E_NOTIMPL;
  switch(EscapeFunction) {
  case ESC_TWAIN_PRIVATE_SUPPORTED_CAPS: // processing TWAIN supported caps Escapecode
     hr = S_OK;
     break;
  default:
     break;
  }

  //
  // If an EscapeFunction code is supported, then first validate the
  // incoming and outgoing buffers.
  //

  if(S_OK == hr) {

     //
     // Validate the incoming data buffer.
     //

     if(IsBadReadPtr(lpInData,cbInDataSize)) {
         hr = E_UNEXPECTED;
     }

     //
     // If the incoming buffer is valid, proceed to validate the
     // outgoing buffer.
     //

     if(S_OK == hr) {
         if(IsBadWritePtr(pOutData,dwOutDataSize)) {
             hr = E_UNEXPECTED;
         } else {

             //
             // Validate the outgoing size pointer.
             //

             if(IsBadWritePtr(pdwActualData,sizeof(DWORD))) {
                 hr = E_UNEXPECTED;
             }
        }
     }

     //
     // Now that buffer validation is complete, proceed to process the
     // proper EscapeFunction code.
     //

     if(S_OK == hr) {

       //
       // Only process a validated EscapeFunction code, and buffers.
       //

       if(EscapeFunction == ESC_TWAIN_PRIVATE_SUPPORTED_CAPS) {

           //
           // Process a TWAIN supported capabilities message.
           //

           // Check the lpInData buffer for the number of bytes
           // of the capability array.
           //
           // 1. Create variable of type LONG*, initializing it
           //    to the value in lpInData.
           // 2. Dereference this variable to obtain the size, in
           //    bytes, of the private TWAIN capability array.

           LONG *pSupportedCapsSize = NULL;
           pSupportedCapsSize = (LONG*)lpInData;

           if(pSupportedCapsSize) {
               LONG lNumBytes = *pSupportedCapsSize;

                // lNumBytes determines the operation to perform.

               if(lNumBytes == 0) {
                // If lNumBytes is zero:
                // a. Create a variable of type LONG*, and
                //    initialize it to the value in pOutData.
                // b. Dereference this variable, and set the size,
                //    in bytes, of the private TWAIN capability array.
                //  c. Set *pchActualData to sizeof(LONG).
                //  d. Set the HRESULT to S_OK, and return.

                  LONG *pCapArraySize = (LONG*)pOutData;
                  *pCapArraySize = (NUM_PRIVATE_TWAIN_CAPS * sizeof(LONG));
                  *pdwActualData = sizeof(LONG);
                   hr = S_OK;
               } else if(lNumBytes > 0) {
                  // If lNumBytes is positive:
                  //  a. Create a variable of type LONG*, and
                  //     initialize it to the value in pOutData.
                  //  b. Dereference this variable, and set each
                  //     capability ID of the private TWAIN capability
                  //     array.
                  //  c. Set *pchActualData to the size, in bytes, of
                  //     the total capability array.
                  //  d. Set the HRESULT to S_OK, and return.

                   LONG *pCapArray = (LONG*)pOutData;
                   pCapArray[0] = ICAP_MY_PRIVATE_CAP1;
                   pCapArray[1] = ICAP_MY_PRIVATE_CAP2;
                   pCapArray[2] = ICAP_MY_PRIVATE_CAP3;
                   pCapArray[3] = ICAP_MY_PRIVATE_CAP4;
                   pCapArray[4] = ICAP_MY_PRIVATE_CAP5;
                   *pdwActualData = (NUM_PRIVATE_TWAIN_CAPS * sizeof(LONG));
                   hr = S_OK;
               } // if (lNumBytes > 0)
           } // if (pSupportedCapsSize)
       }
     }
  }

  //
  // If your driver will not support this entry point, then
  // it must return E_NOTIMPL (error, not implemented).
  //

  return hr;
}
```

 

