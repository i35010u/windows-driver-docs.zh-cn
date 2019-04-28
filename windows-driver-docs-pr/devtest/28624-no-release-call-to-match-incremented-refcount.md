---
title: C28624
description: 警告 C28624 否调用 release （） 以 LResultFromObject 中递增的 refcount 匹配。
ms.assetid: e769d232-ef6e-4b70-8cac-f4dd43807e1d
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28624
ms.openlocfilehash: 115bc9a5f20f0612b51d05286c67456056a9b109
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347056"
---
# <a name="c28624"></a>C28624


警告 C28624:不需要调用 release （） 以 LResultFromObject 中递增的 refcount 匹配

**LresultFromObject**会增加对新的 IAccessible 对象的引用计数。

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

 

 





