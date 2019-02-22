---
title: 创建回调对象示例
description: 创建回调对象示例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- 回调对象 WDK UMDF，创建的示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19f852def4de16f87cef0b970f1ed39e78ca9024
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555831"
---
# <a name="creating-callback-objects-example"></a>创建回调对象示例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下面的代码示例演示如何将驱动程序的实现中创建设备回调对象及其[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法然后将指针传递给设备回调对其调用中的接口[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)方法来创建的设备。

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

 

 





