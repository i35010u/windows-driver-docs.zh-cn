---
title: 在 WIA 设备上进行诊断
description: 在 WIA 设备上进行诊断
ms.assetid: 15962c49-f03c-409b-b138-033893a50ec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e1d6f947f301bfb8688ccd282fa0aa827826f3e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192597"
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

 

