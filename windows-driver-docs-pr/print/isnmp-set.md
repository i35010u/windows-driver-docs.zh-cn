---
title: ISNMP Set 方法
description: Set 方法启用 ASP Web 页后，可以将一个值与 SNMP OID 相关联。
MS-HAID:
- webfnc\_b0392f7d-7d17-41ce-97fe-8f8baa691c78.xml
- print.isnmp\_set
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 7eac82e7-3f19-4eda-8706-eac6aa2b8dae
keywords:
- Set 方法打印设备
- Set 方法打印设备 ISNMP 接口
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
ms.openlocfilehash: 2d1bd97050f50ef5169bab0e77c119f8a69dc3ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543981"
---
# <a name="isnmpset-method"></a>ISNMP::Set 方法

`Set`方法启用 ASP Web 页后，可以将一个值与 SNMP OID 相关联。

<a name="syntax"></a>语法
------

```cpp
HRESULT Set(
  [in]  BSTR    bstrOID,
  [out] VARIANT varValue
);
```

<a name="parameters"></a>参数
----------

*bstrOID* \[in\]  
调用方提供指向 SNMP OID 字符串指针。

*varValue* \[out\]  
调用方提供的位置包含 OID 的值。

<a name="return-value"></a>返回值
------------

此外可以返回 Win32 错误代码。

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

此方法调用**SnmpMgrRequest**函数来设置 SNMP OID 值。 有关详细信息，请参阅 Windows SDK 文档。

[ **ISNMP::Open** ](isnmp-open.md)前必须调用方法`ISNMP::Set`可以调用方法。

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
<td>桌面设备</td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Olesnmp.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**ISNMP::Open**](isnmp-open.md)
