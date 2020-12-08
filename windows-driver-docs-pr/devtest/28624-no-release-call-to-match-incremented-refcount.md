---
title: C28624
description: '警告 C28624 不会对 Release ( 调用 # A1，以匹配 LResultFromObject 中增加的引用计数。'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28624
ms.openlocfilehash: d800bde479e73143773101290df3dbd0fc5c8e62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795625"
---
# <a name="c28624"></a>C28624


警告 C28624：不调用 Release ( # A1，以匹配 LResultFromObject 中的递增引用计数

**LresultFromObject** 增加了新 IAccessible 对象上的引用计数。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例将生成此警告。

```
{
 IAccessible *pacc = CreateNewIAccessible();
 LRESULT lTemp = LresultFromObject(riid, NULL, pacc );
}

{
 IAccessible *pacc = NULL;
 // Get new interface (from same object)
 QueryInterface( & pacc );

 // Lresult will internally bump up the refcount
 // to hold onto the object.
 
 LRESULT lTemp = LresultFromObject( riid, NULL, pacc );
}
```

下面的示例可避免此错误。

```
{
 IAccessible *pacc = CreateNewIAccessible();
 // Lresult internally increases the refcount to
 // hold onto the object.
 LRESULT lTemp = LresultFromObject(riid, NULL, pacc );

 // We no longer need our pacc interface, so we release it.

 pacc->Release();
}
```

 

 





