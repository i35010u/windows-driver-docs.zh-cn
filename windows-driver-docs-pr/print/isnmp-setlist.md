---
title: ISNMP 中方法
description: 中方法，以将值与 SNMP Oid 数组相关联的 ASP Web 页。
MS-HAID:
- webfnc\_56e01eeb-9b33-4f32-b209-cde82d78e2d5.xml
- print.isnmp\_setlist
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: c783fc1b-e354-4b79-a57d-975ce0d0a0a4
keywords:
- 中方法打印设备
- 中方法打印设备，ISNMP 接口
- ISNMP 接口中方法的打印设备
topic_type:
- apiref
api_name:
- ISNMP.SetList
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14bf2f148594d30cf958d846c12f933f5f8d3321
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345283"
---
# <a name="isnmpsetlist-method"></a>ISNMP::SetList 方法

`SetList`方法启用 ASP Web 页后，可以将值与 SNMP Oid 数组相关联。

<a name="syntax"></a>语法
------

```cpp
HRESULT SetList(
  [in] VARIANT *varName,
  [in] VARIANT *varValue
);
```

<a name="parameters"></a>Parameters
----------

*varName* \[in\]  
调用方提供的 SNMP OID 字符串数组指针。

*varValue* \[in\]  
调用方提供指向数组的 OID 值。

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

此方法调用**SnmpMgrRequest**函数来设置 SNMP OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

[ **ISNMP::Open** ](isnmp-open.md)前必须调用方法`ISNMP::SetList`可以调用方法。

```vb
Dim StrIP, strCommunity, objSNMP, OIDArray, OIDValueArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDArray = Array("25.3.2.1.5", "25.3.5.1.1")
...
' Determine values to assign to OIDs; store them in OIDArray.
...
OIDValueArray = objSNMP.SetList (OIDArray)
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
