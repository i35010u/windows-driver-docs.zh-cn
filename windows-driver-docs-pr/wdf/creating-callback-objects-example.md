---
title: 创建回调对象示例
description: 创建回调对象示例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- 回叫对象 WDK UMDF，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327c02d71a27bbe41851883dfced880ca614470e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845603"
---
# <a name="creating-callback-objects-example"></a>创建回调对象示例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下面的代码示例演示了驱动程序如何在其[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法的实现中创建设备回调对象，然后在调用[**IWDFDriver：： CreateDevice 的情况下将该指针传递到设备回调接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)用于创建设备的方法。

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

 

 





