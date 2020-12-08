---
title: 用于设置自定义属性的示例代码
description: 用于设置自定义属性的示例代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b7dbc3613ef465e2b54558041d7cc880c51569f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840711"
---
# <a name="sample-code-to-set-custom-properties"></a>用于设置自定义属性的示例代码





若要设置自定义属性，您的应用程序或自定义 UI 可能具有如下所示的代码：

```cpp
    IWiaPropertyStorage *pItemPropertyStorage = NULL;
 
    //
    //  Get the item's Property Storage
    //
    hr = pMyItem->QueryInterface(IID_IWiaPropertyStorage, (void**)&pItemPropertyStorage);
    if (SUCCEEDED(hr)) {

 
  //
  //  Variables to store the property value and identifier.
  //

  PROPVARIANT pvMyProperty;   // PropVariant to store property value.
  PROPSPEC    psMyProperty;   // PropSpec that identifies the property.
 
  psMyProperty.ulKind = PRSPEC_PROPID;
  psMyProperty.propid = myCustomPropID;   
  //  This should be the same value 
  //  that your driver has.  The
  //  best practice is to put a
  //  define in a header file
  //  that is common to driver
  //  and UI or the application components.
 
  //
  //  Initialize the PropVariant.
  //
  PropVariantInit(&pvMyProperty);
 
  //
  //  Fill in the property value.
  //  This example fills in the number 7 to a LONG type.
  //
  pvMyProperty.vt     = VT_I4;
  pvMyProperty.lVal   = 7;
 
  //
  //  Write the property value.
  //
  hr = pItemPropertyStorage->WriteMultiple(1,
                               &psMyProperty,
                               &pvMyProperty,
                                          0);
  //
  //  Etc.  
  //
  .
  .
  .
    }
```

 

 




