---
title: 创建回调对象示例
description: 创建回调对象示例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- 回叫对象 WDK UMDF，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007819ea908899d616e46daa84d398f00a11beb2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192118"
---
# <a name="creating-callback-objects-example"></a>创建回调对象示例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

下面的代码示例演示驱动程序如何在其 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法的实现中创建设备回调对象，然后在其对 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice) 方法的调用中将指针传递到设备回调接口，以创建设备。

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

 

