---
title: WDF_DECLARE_CONTEXT_TYPE 宏
description: WDF_DECLARE_CONTEXT_TYPE 宏为驱动程序的对象特定上下文空间创建一个名称和一个访问器方法。
ms.assetid: 5fd9950e-943a-4340-b8f1-125343effdf7
keywords:
- WDF_DECLARE_CONTEXT_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ed65ea0585d3489bc42dc27133cce935a8b487
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185703"
---
# <a name="wdf_declare_context_type-macro"></a>WDF_DECLARE_CONTEXT_TYPE 宏


\[适用于 KMDF 和 UMDF\]

WDF_DECLARE_CONTEXT_TYPE 宏为驱动程序的对象特定上下文空间创建一个名称和一个访问器方法。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_DECLARE_CONTEXT_TYPE(
    _contexttype
);
```

<a name="parameters"></a>参数
----------

*_contexttype*   
驱动程序定义的结构的结构类型名称，该结构描述对象的上下文空间的内容。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

有关使用此宏的详细信息，请参阅 [框架对象上下文空间](./framework-object-context-space.md)。

<a name="examples"></a>示例
--------

下面的代码示例定义请求对象 MY_REQUEST_CONTEXT) 的上下文结构，注册该结构，然后调用 WDF_DECLARE_CONTEXT_TYPE 宏 (。 宏为上下文结构创建访问器方法，并将该方法命名为 **WdfObjectGet_MY_REQUEST_CONTEXT**。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(MY_REQUEST_CONTEXT)
```

下面的代码示例创建一个请求对象，然后使用 **WdfObjectGet_MY_REQUEST_CONTEXT** 访问器方法获取指向该对象的上下文空间的指针。

```cpp
WDFREQUEST Request;
WDF_OBJECT_ATTRIBUTES MyRequestObjectAttributes;
PMY_REQUEST_CONTEXT pMyContext;

WDF_OBJECT_ATTRIBUTES_INIT(&MyRequestObjectAttributes);
WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
                                       &MyRequestObjectAttributes,
                                       MY_REQUEST_CONTEXT
                                       );
status = WdfRequestCreate(
                          &MyRequestObjectAttributes
                          NULL,
                          &Request
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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WdfObjectGetTypedContext**](wdfobjectgettypedcontext.md)

[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)

 

