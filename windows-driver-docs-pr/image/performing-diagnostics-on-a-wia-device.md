---
title: 在 WIA 设备上进行诊断
description: 在 WIA 设备上进行诊断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff088b699e14dbc7af1dd17268e449fcf3786ba2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841089"
---
# <a name="performing-diagnostics-on-a-wia-device"></a>在 WIA 设备上进行诊断





WIA 服务可以通过调用 [**IStiUSD：:D 诊断**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic) 方法来测试设备的功能状态。 WIA 微型驱动程序应检查硬件的当前功能状态并报告结果。 当在 WIA 设备的默认属性 (页上按下 "测试设备" 按钮时，还将调用 **IStiUSD：:D 诊断** 方法，) Microsoft 提供的属性页。

下面的示例演示 **IStiUSD：:D 诊断** 方法的实现。

```cpp
STDMETHODIMP CWIADevice::Diagnostic(LPSTI_DIAG pBuffer)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if(!pBuffer){
     return E_INVALIDARG;
  }

  //
  // initialize response buffer
  //

  memset(&pBuffer->sErrorInfo,0,sizeof(pBuffer->sErrorInfo));

  pBuffer->sErrorInfo.dwGenericError = NOERROR;
  pBuffer->sErrorInfo.dwVendorError  = 0;

  HRESULT hr = S_OK;
  if(!TestMyDeviceFunctionalty()) {
    pBuffer->sErrorInfo.dwGenericError = E_FAIL; // win32 generic error code
    pBuffer->sErrorInfo.dwVendorError  = 1234;   // device specific vendor error code
  }
  return hr;
}
```

 

