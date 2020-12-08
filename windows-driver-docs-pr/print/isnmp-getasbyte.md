---
title: ISNMP GetAsByte 方法
description: 使用 GetAsByte 方法可以获取由 SNMP OID 标识的值并将该值转换为无符号整数。
MS-HAID:
- webfnc\_915155f7-8444-4824-88be-808f10a9ff8e.xml
- print.isnmp\_getasbyte
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- GetAsByte 方法打印设备
- GetAsByte 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，GetAsByte 方法
topic_type:
- apiref
api_name:
- ISNMP.GetAsByte
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8475e8a04e199630cf5374fd20f419aefde3dd7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796529"
---
# <a name="isnmpgetasbyte-method"></a>ISNMP：： GetAsByte 方法

使用 `GetAsByte` 方法，ASP 网页可以获取由 SNMP OID 标识的值并将该值转换为无符号整数。

<a name="syntax"></a>语法
------

```cpp
HRESULT GetAsByte(
  [in]  BSTR  bstrOID,
  [out] PUINT puValue
);
```

<a name="parameters"></a>参数
----------

*bstrOID* \[中\]  
调用方提供的包含 SNMP OID 的 BSTR 值。

*puValue* \[弄\]  
调用方提供的指向接收无符号整数值的位置的指针。

<a name="return-value"></a>返回值
------------

此方法返回下表中的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>S_OK</strong></td>
<td><p>操作成功。</p></td>
</tr>
<tr class="even">
<td><strong>E_FAIL</strong></td>
<td><p>未调用 <strong>ISNMP：： Open</strong> 方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_INVALIDARG</strong></td>
<td><p>指定的 SNMP OID 无效。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法调用 **SnmpMgrRequest** 函数来检索由 SNMP OID 标识的值。 在方法将值传递给调用方之前，它将调用方转换为无符号整数。 有关 **SnmpMgrRequest** 的详细信息，请参阅 Windows SDK 文档。

对于以下数据类型，该 `ISNMP::GetAsByte` 方法将由 SNMP OID 标识的标量值转换为调用方收到的等效无符号整数值：

-   ASN \_ 整数

-   ASN \_ RFC1155 \_ 计数器

-   ASN \_ RFC1155 \_ 仪表

-   ASN \_ RFC1155 \_ TIMETICKS

-   ASN \_ UNSIGNED32

对于以下数据类型，如果由 SNMP OID 标识的值的大小不超过两个字节，则该方法会将字符串、数组或不透明值的开头元素打包到调用方接收的无符号整数值中：

-   ASN \_ 位

-   ASN \_ OCTETSTRING

-   ASN \_ RFC1155 不 \_ 透明

-   ASN \_ 序列

此方法当前不支持除前面的列表中的数据类型之外的其他数据类型的转换。 有关这些数据类型的详细信息，请参阅 Windows SDK 文档中的 SNMP 管理 API 的说明。

必须先调用 [**ISNMP：： Open**](isnmp-open.md) 方法，然后才能 `ISNMP::GetAsByte` 调用方法。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValue
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDValue = objSNMP.GetAsByte ("25.3.5.1.2")
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
<td>台式机</td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Olesnmp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**ISNMP：： Open**](isnmp-open.md)
