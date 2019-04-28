---
title: 在 WIA 设备上进行诊断
description: 在 WIA 设备上进行诊断
ms.assetid: 15962c49-f03c-409b-b138-033893a50ec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ff78cc4d2a51078109eee2589dbdcb94ed44d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327849"
---
# <a name="performing-diagnostics-on-a-wia-device"></a>在 WIA 设备上进行诊断





WIA 服务可以通过调用测试设备的功能状态[ **IStiUSD::Diagnostic** ](https://msdn.microsoft.com/library/windows/hardware/ff543814)方法。 WIA 微型驱动程序应检查硬件的当前正常运行状态，并报告结果。 **IStiUSD::Diagnostic** WIA 设备的默认属性页 （由 Microsoft 提供的属性页上） 上按"测试设备"按钮时，也会调用方法。

下面的示例演示的实现**IStiUSD::Diagnostic**方法。

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

 

 




