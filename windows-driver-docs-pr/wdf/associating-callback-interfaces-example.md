---
title: 将相关联回调接口的示例
description: 将相关联回调接口的示例
ms.assetid: 6156730b-394c-451c-beea-1b25ba5a1fe3
keywords:
- 回调对象 WDK UMDF
- 回调接口 WDK UMDF
- 将相关联回调接口 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f4be15bd42f67d4256b3917a9e1fabe33f5ed5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547041"
---
# <a name="associating-callback-interfaces-example"></a>将相关联回调接口的示例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

以下代码示例演示如何将驱动程序实现到使用该驱动程序的创建实例方法[创建设备回调对象](creating-callback-objects-example.md)。 该驱动程序分配的回调上下文并将提供相关联**IUnknown**具有一个或多个回调接口。 可以随后使用该框架**QueryInterface**发现驱动程序支持的回调接口。

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

 

 





