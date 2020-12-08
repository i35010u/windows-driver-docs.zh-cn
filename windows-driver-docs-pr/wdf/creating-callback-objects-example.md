---
title: 创建回调对象示例
description: 创建回调对象示例
keywords:
- 回叫对象 WDK UMDF，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8805b565f1c6c2389c858810d67f29aa37c788c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829015"
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

 

