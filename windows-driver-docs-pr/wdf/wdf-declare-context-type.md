---
title: WDF_DECLARE_CONTEXT_TYPE 宏
description: WDF_DECLARE_CONTEXT_TYPE 宏创建的名称和驱动程序的特定于对象上下文空间的访问器方法。
ms.assetid: 5fd9950e-943a-4340-b8f1-125343effdf7
keywords:
- WDF_DECLARE_CONTEXT_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2193b23abfdd8a60a670fc14b627fbf1faf919
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562283"
---
# <a name="wdfdeclarecontexttype-macro"></a>WDF_DECLARE_CONTEXT_TYPE 宏


\[适用于 KMDF 和 UMDF\]

WDF_DECLARE_CONTEXT_TYPE 宏创建的名称和驱动程序的特定于对象上下文空间的访问器方法。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_DECLARE_CONTEXT_TYPE(
    _contexttype
);
```

<a name="parameters"></a>Parameters
----------

*_contexttype*   
描述对象的上下文空间的内容的驱动程序定义的结构结构类型名称。

<a name="return-value"></a>返回值
------------

此宏不会返回一个值。

<a name="remarks"></a>备注
-------

有关使用此宏的详细信息，请参阅[框架对象上下文空间](https://msdn.microsoft.com/library/windows/hardware/ff542873)。

<a name="examples"></a>示例
--------

下面的代码示例定义一个请求对象的上下文结构 (MY_REQUEST_CONTEXT)、 注册结构，并调用 WDF_DECLARE_CONTEXT_TYPE 宏。 宏会创建一个访问器方法的上下文结构和名称的方法**WdfObjectGet_MY_REQUEST_CONTEXT**。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(MY_REQUEST_CONTEXT)
```

下面的代码示例创建一个请求对象，并使用它**WdfObjectGet_MY_REQUEST_CONTEXT**访问器方法来获取对象的上下文空间的指针。

```cpp
WDFREQUEST Request;
WDF_OBJECT_ATTRIBUTES MyRequestObjectAttributes;
PMY_REQUEST_CONTEXT pMyContext;

WDF_OBJECT_ATTRIBUTES_INIT(&amp;MyRequestObjectAttributes);
WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
                                       &amp;MyRequestObjectAttributes,
                                       MY_REQUEST_CONTEXT
                                       );
status = WdfRequestCreate(
                          &amp;MyRequestObjectAttributes
                          NULL,
                          &amp;Request
                          );
if (!NT_SUCCESS(status)) {
    return status;
}
pMyContext = WdfObjectGet_MY_REQUEST_CONTEXT(Request);
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WdfObjectGetTypedContext**](wdfobjectgettypedcontext.md)

[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)

 

 






