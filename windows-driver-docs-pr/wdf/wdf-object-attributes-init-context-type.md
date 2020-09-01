---
title: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏
description: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏可初始化驱动程序的 WDF_OBJECT_ATTRIBUTES 结构，并将对象的驱动程序定义的上下文信息插入到结构中。
ms.assetid: 83e397b1-e37d-451d-9007-3b34993187c3
keywords:
- WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d26760781adbf79961f4ab57c11b86f4698b9341
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188123"
---
# <a name="wdf_object_attributes_init_context_type-macro"></a>WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏


\[适用于 KMDF 和 UMDF\]

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**宏可初始化驱动程序的[**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构，并将对象的驱动程序定义的上下文信息插入到结构中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(
    _attributes,
    _contexttype
);
```

<a name="parameters"></a>参数
----------

*_attributes*   
指向 [**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构的指针。

*_contexttype*   
驱动程序定义的结构的结构类型名称，该结构描述对象的上下文空间的内容。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>注解
-------

在调用 **WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**之前，必须 [**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md) 或 [**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md) 全局 (不在函数) 中。

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**宏结合了[**WDF_OBJECT_ATTRIBUTES_INIT**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)函数和[**WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE**](wdf-object-attributes-set-context-type.md)的宏。

<a name="examples"></a>示例
--------

下面的代码示例定义 WDM_NDIS_REQUEST 的上下文结构。 然后，该示例调用 [**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md) 宏来注册结构，并指定上下文访问器方法将命名为 **RequestGetMyContext**。 然后，在函数中，该示例分配一个 [**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构，然后初始化 **WDF_OBJECT_ATTRIBUTES** 结构。

```cpp
typedef struct _WDM_NDIS_REQUEST
{
   PMP_ADAPTER  Adapter;
   NDIS_OID  Oid;
   NDIS_REQUEST_TYPE  RequestType;
   PVOID  InformationBuffer;
   ULONG  InformationBufferLength;
   PULONG  BytesReadOrWritten;
   PULONG  BytesNeeded;
} WDM_NDIS_REQUEST, *PWDM_NDIS_REQUEST;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(WDM_NDIS_REQUEST, RequestGetMyContext);

// above are in global space

...

WDF_OBJECT_ATTRIBUTES  attributes;

WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE( &attributes, WDM_NDIS_REQUEST );
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
<td><p>Header</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)

[**WDF_OBJECT_ATTRIBUTES_INIT**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)

[**WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE**](wdf-object-attributes-set-context-type.md)

 

