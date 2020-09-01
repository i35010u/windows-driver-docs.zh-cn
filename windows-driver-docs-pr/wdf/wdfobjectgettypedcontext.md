---
title: WdfObjectGetTypedContext 宏
description: WdfObjectGetTypedContext 宏返回指向对象的上下文空间的指针。
ms.assetid: de0edae4-7c05-4419-972e-c106875dfff1
keywords:
- WdfObjectGetTypedContext 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 734781fba81f889a96acc7d43426110cf74628f3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187990"
---
# <a name="wdfobjectgettypedcontext-macro"></a>WdfObjectGetTypedContext 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectGetTypedContext**宏返回指向对象的上下文空间的指针。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID WdfObjectGetTypedContext(
    Handle,
    Type
);
```

<a name="parameters"></a>参数
----------

*柄*   
框架对象的句柄。

*类别*   
描述对象的上下文空间的驱动程序定义的结构的符号名称。

<a name="return-value"></a>返回值
------------

**WdfObjectGetTypedContext** 返回指向指定对象的上下文空间的指针。

<a name="remarks"></a>备注
-------

可以使用 **WdfObjectGetTypedContext** 宏获取指向任何框架对象上下文空间的指针。 使用此宏作为调用 [**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md) 宏或 [**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md) 宏创建的对象特定上下文访问器方法的替代方法。 请注意，如果您使用 **WdfObjectGetTypedContext**，则仍必须使用 WDF_DECLARE_CONTEXT_TYPE 或 WDF_DECLARE_CONTEXT_TYPE_WITH_NAME 来声明您的对象上下文。

有关这些宏的详细信息，请参阅 [框架对象上下文空间](./framework-object-context-space.md)。

<a name="examples"></a>示例
--------

下面的代码示例定义请求对象的上下文结构 (MY_REQUEST_CONTEXT) ，然后注册该结构。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(MY_REQUEST_CONTEXT)
```

下面的代码示例创建一个请求对象并获取指向其上下文空间的指针。

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
<tr class="odd">
<td><p>库</p></td>
<td>Wdf01000.sys (KMDF) ;WUDFx02000.dll (UMDF) </td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)

 

