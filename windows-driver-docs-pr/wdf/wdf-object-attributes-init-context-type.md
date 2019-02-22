---
title: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏
description: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏初始化驱动程序的 WDF_OBJECT_ATTRIBUTES 结构，并插入结构对象的驱动程序定义的上下文信息。
ms.assetid: 83e397b1-e37d-451d-9007-3b34993187c3
keywords:
- WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805172577296774d3128f90c719d07b9ebd63d2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555490"
---
# <a name="wdfobjectattributesinitcontexttype-macro"></a>WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE 宏


\[适用于 KMDF 和 UMDF\]

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**宏初始化的驱动程序[ **WDF_OBJECT_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构，并将插入对象的驱动程序定义的上下文到结构的信息。

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
一个指向[ **WDF_OBJECT_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构。

*_contexttype*   
描述对象的上下文空间的内容的驱动程序定义的结构结构类型名称。

<a name="return-value"></a>返回值
------------

此宏不会返回一个值。

<a name="remarks"></a>备注
-------

然后再调用**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**，则必须调用[ **WDF_DECLARE_CONTEXT_TYPE** ](wdf-declare-context-type.md)或者[ **WDF_DECLARE_CONTEXT_TYPE_WITH_NAME** ](wdf-declare-context-type-with-name.md)全局范围内 （而不是在某个函数）。

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**宏将合并[ **WDF_OBJECT_ATTRIBUTES_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552402)函数和[ **WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE** ](wdf-object-attributes-set-context-type.md)宏。

<a name="examples"></a>示例
--------

下面的代码示例定义 WDM_NDIS_REQUEST 上下文结构。 然后，该示例调用[ **WDF_DECLARE_CONTEXT_TYPE_WITH_NAME** ](wdf-declare-context-type-with-name.md)宏进行注册，该结构和指定的上下文访问器方法将被命名为**RequestGetMyContext**. 然后，在函数中，示例分配[ **WDF_OBJECT_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构，然后初始化**WDF_OBJECT_ATTRIBUTES**结构。

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

WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE( &amp;attributes, WDM_NDIS_REQUEST );
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
<td><p>标头</p></td>
<td>Wdfobject.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WDF_OBJECT_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff552400)

[**WDF_OBJECT_ATTRIBUTES_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552402)

[**WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE**](wdf-object-attributes-set-context-type.md)

 

 






