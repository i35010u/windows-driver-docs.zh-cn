---
title: 创建回调对象示例
description: 创建回调对象示例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- 回调对象 WDK UMDF，创建的示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca08be818e342e761830418ff1183e64a1fd6f56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382393"
---
# <a name="creating-callback-objects-example"></a>创建回调对象示例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下面的代码示例演示如何将驱动程序的实现中创建设备回调对象及其[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法然后将指针传递给设备回调对其调用中的接口[ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法来创建的设备。

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

 

 





