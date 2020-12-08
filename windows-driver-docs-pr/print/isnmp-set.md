---
title: ISNMP Set 方法
description: Set 方法使 ASP 网页可以将值与 SNMP OID 关联起来。
MS-HAID:
- webfnc\_b0392f7d-7d17-41ce-97fe-8f8baa691c78.xml
- print.isnmp\_set
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 设置方法打印设备
- 设置方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，Set 方法
topic_type:
- apiref
api_name:
- ISNMP.Set
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2537aeeade6a745d5f89566ae7b2483f33b77e9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796517"
---
# <a name="isnmpset-method"></a>ISNMP：： Set 方法

`Set`使用方法，ASP 网页可以将值与 SNMP OID 关联起来。

<a name="syntax"></a>语法
------

```cpp
HRESULT Set(
  [in]  BSTR    bstrOID,
  [out] VARIANT varValue
);
```

<a name="parameters"></a>参数
----------

*bstrOID* \[中\]  
调用方提供的指向 SNMP OID 字符串的指针。

*varValue* \[弄\]  
调用方提供的包含 OID 值的位置。

<a name="return-value"></a>返回值
------------

也可以返回 Win32 错误代码。

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

此方法调用 **SnmpMgrRequest** 函数来设置 SNMP OID 值。 有关详细信息，请参阅 Windows SDK 文档。

必须先调用 [**ISNMP：： Open**](isnmp-open.md) 方法，然后才能 `ISNMP::Set` 调用方法。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValue
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
...
' Determine value to assign to OID; store it in OIDValue.
...
objSNMP.Set ("43.18.1.1.2", OIDValue)
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
