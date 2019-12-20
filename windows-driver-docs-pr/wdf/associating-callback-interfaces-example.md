---
title: 关联回调接口示例
description: 关联回调接口示例
ms.assetid: 6156730b-394c-451c-beea-1b25ba5a1fe3
keywords:
- 回叫对象 WDK UMDF
- 回调接口 WDK UMDF
- 关联回拨接口 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bf28b0466225189fec2c07eac7560a6a92d486
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210045"
---
# <a name="associating-callback-interfaces-example"></a>关联回调接口示例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

下面的代码示例演示驱动程序如何实现一个创建实例方法，驱动程序使用该方法[创建设备回调对象](creating-callback-objects-example.md)。 驱动程序分配回调上下文，并将提供的**IUnknown**与一个或多个回调接口相关联。 然后，框架可以使用**QueryInterface**来发现驱动程序所支持的回调接口。

```cpp
static HRESULT CreateInstance(
                  IUnknown **ppUnknown, 
                  IWDFDeviceInitialize *pDeviceInit,
                  HANDLE CompletionPort 
                  ) {
   ...
   // Allocate the callback context
   CMyDevice *pMyDevice = new CMyDevice();
   ...
   HRESULT hr;
   // Discover the callback interface
   hr = pMyDevice->QueryInterface( 
                      __uuidof(IUnknown), 
                      (void **) ppUnknown
                      );
   ...
   return hr;
}
```

 

 





