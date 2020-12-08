---
title: WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 宏
description: WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 宏为驱动程序的对象特定上下文空间创建一个具有指定名称的访问器方法。
keywords:
- WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7000662052ccc3aca8d86fc3b903aa920ef48d20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809789"
---
# <a name="wdf_declare_context_type_with_name-macro"></a>WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 宏


\[适用于 KMDF 和 UMDF\]

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 宏为驱动程序的对象特定上下文空间创建一个具有指定名称的访问器方法。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(
    _contexttype,
    _castingfunction
);
```

<a name="parameters"></a>参数
----------

*_contexttype*   
驱动程序定义的结构的结构类型名称，该结构描述对象的上下文空间的内容。

*_castingfunction*   
C 语言例程名称。 宏使用此名称作为为对象的上下文空间创建的访问器方法的名称。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

有关使用此宏的详细信息，请参阅 [框架对象上下文空间](./framework-object-context-space.md)。

<a name="examples"></a>示例
--------

下面的代码示例定义请求对象的上下文结构 (MY_REQUEST_CONTEXT) 。 然后，该示例调用 WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 宏来注册结构，并指定上下文访问器方法将命名为 **RequestGetMyContext**。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(MY_REQUEST_CONTEXT, RequestGetMyContext)
```

下面的代码示例创建一个请求对象，然后使用 **RequestGetMyContext** 访问器方法获取指向该对象的上下文空间的指针。

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

pMyContext = RequestGetMyContext(Request);
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

## <a name="see-also"></a>请参阅


[**WdfObjectGetTypedContext**](wdfobjectgettypedcontext.md)

[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

 

