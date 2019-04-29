---
title: ISNMP GetAsByte 方法
description: GetAsByte 方法，以获取标识 SNMP OID 的值，并将值转换为无符号整数的 ASP Web 页。
MS-HAID:
- webfnc\_915155f7-8444-4824-88be-808f10a9ff8e.xml
- print.isnmp\_getasbyte
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 0a9d170d-486f-49e9-a8f9-c0d8b17f681b
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
ms.openlocfilehash: 2daf9bf51c6ec3f814aa188616d26538f583e493
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384191"
---
# <a name="isnmpgetasbyte-method"></a>ISNMP::GetAsByte 方法

`GetAsByte`方法允许 ASP Web 页面以获取标识 SNMP OID 的值，并将值转换为无符号整数。

<a name="syntax"></a>语法
------

```cpp
HRESULT GetAsByte(
  [in]  BSTR  bstrOID,
  [out] PUINT puValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrOID* \[in\]  
调用方提供 BSTR 值，该值包含 SNMP OID。

*puValue* \[out\]  
指向接收的无符号的整数值的位置的调用方提供的指针。

<a name="return-value"></a>返回值
------------

下表中，此方法返回的值之一。

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
<td><p><strong>ISNMP::Open</strong>尚未调用方法。</p></td>
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

此方法调用**SnmpMgrRequest**函数以检索标识 SNMP OID 的值。 该方法将值传递给调用方之前，它将调用方转换为无符号整数。 有关详细信息**SnmpMgrRequest**，请参阅 Windows SDK 文档。

对于以下数据类型，`ISNMP::GetAsByte`方法将转换为等效的无符号的整数值，调用方会接收 SNMP OID 标识的标量值：

-   ASN\_INTEGER

-   ASN\_RFC1155\_计数器

-   ASN\_RFC1155\_GAUGE

-   ASN\_RFC1155\_的 TIMETICKS

-   ASN\_UNSIGNED32

对于以下数据类型，如果 SNMP OID 标识的值的大小不超过两个字节，该方法包的开始元素的字符串、 数组或不透明值到调用方会接收的无符号的整数值：

-   ASN\_BITS

-   ASN\_OCTETSTRING

-   ASN\_RFC1155\_OPAQUE

-   ASN\_序列

此方法当前不支持从中前面的列以外的数据类型的转换。 有关这些数据类型的详细信息，请参阅 Windows SDK 文档中的 SNMP 管理 API 的说明。

[ **ISNMP::Open** ](isnmp-open.md)前必须调用方法`ISNMP::GetAsByte`可以调用方法。

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
<td>桌面设备</td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Olesnmp.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**ISNMP::Open**](isnmp-open.md)
