---
title: 创建回调对象示例
description: 创建回调对象示例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- 回叫对象 WDK UMDF，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 826efa4bca1593569ac46755fb74a0b06178727f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210221"
---
# <a name="creating-callback-objects-example"></a>创建回调对象示例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

下面的代码示例演示驱动程序如何在其[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法的实现中创建设备回调对象，然后在其对[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法的调用中将指针传递到设备回调接口，以创建设备。

```cpp
   HRESULT CMyDriver::OnDeviceAdd(
              IWDFDriver*           pDriver,
              IWDFDeviceInitialize* pDeviceInit
              ) {
      IUnknown *pDeviceCallback = NULL;
      ...
      HRESULT hr;
      // Create callback object
      hr = CMyDevice::CreateInstance( &pDeviceCallback,
                                      pDeviceInit,
                                      completionPort );
      ...
      // Create WDF device
      hr = pDriver->CreateDevice( pDeviceInit, 
                                  pDeviceCallback,
                                  &pIWDFDevice );
      ...
   }
```

 

 





