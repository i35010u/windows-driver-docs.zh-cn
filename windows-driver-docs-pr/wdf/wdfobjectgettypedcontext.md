---
title: WdfObjectGetTypedContext macro
description: WdfObjectGetTypedContext 宏返回一个指向对象的上下文空间。
ms.assetid: de0edae4-7c05-4419-972e-c106875dfff1
keywords:
- WdfObjectGetTypedContext macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a7da5dda6976c161246f119a8865a1ced002d4a
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161373"
---
# <a name="wdfobjectgettypedcontext-macro"></a>WdfObjectGetTypedContext macro


\[适用于 KMDF 和 UMDF\]

**WdfObjectGetTypedContext**宏将指针返回到对象上下文空间。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID WdfObjectGetTypedContext(
    Handle,
    Type
);
```

<a name="parameters"></a>Parameters
----------

*句柄*   
Framework 对象的句柄。

*类型*   
描述对象的上下文空间的驱动程序定义的结构的符号名称。

<a name="return-value"></a>返回值
------------

**WdfObjectGetTypedContext**将指针返回到指定的对象的上下文空间。

<a name="remarks"></a>备注
-------

可以使用**WdfObjectGetTypedContext**宏，以获取任何框架对象上下文空间的指针。 使用此宏，因为调用特定于对象上下文访问器方法的替代方法由创建[ **WDF_DECLARE_CONTEXT_TYPE** ](wdf-declare-context-type.md)宏或[ **WDF_DECLARE_CONTEXT_TYPE_WITH_NAME** ](wdf-declare-context-type-with-name.md)宏。 请注意，如果您使用**WdfObjectGetTypedContext**，仍必须使用 WDF_DECLARE_CONTEXT_TYPE 或 WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 来声明对象上下文。

有关这些宏的详细信息，请参阅[框架对象上下文空间](https://msdn.microsoft.com/library/windows/hardware/ff542873)。

<a name="examples"></a>示例
--------

下面的代码示例定义一个请求对象的上下文结构 (MY_REQUEST_CONTEXT)，然后注册结构。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(MY_REQUEST_CONTEXT)
```

下面的代码示例创建一个请求对象，并获取指向其上下文空间的指针。

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
                          &MyRequestObjectAttributes,
                          NULL,
                          &Request
                          );

if (!NT_SUCCESS(status)) {
    return status;
}
pMyContext = WdfObjectGetTypedContext(
                                      Request,
                                      MY_REQUEST_CONTEXT
                                      );
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
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000.sys (KMDF); WUDFx02000.dll (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)

 

 






