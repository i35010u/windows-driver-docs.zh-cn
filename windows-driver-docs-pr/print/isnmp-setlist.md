---
title: ISNMP SetList 方法
description: 使用 SetList 方法，ASP 网页可以将值与 SNMP Oid 数组关联起来。
MS-HAID:
- webfnc\_56e01eeb-9b33-4f32-b209-cde82d78e2d5.xml
- print.isnmp\_setlist
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- SetList 方法打印设备
- SetList 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，SetList 方法
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
ms.openlocfilehash: e79ffbe744e9287e39b8514ea225b5ec20e6a6b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835501"
---
# <a name="isnmpsetlist-method"></a>ISNMP：： SetList 方法

使用 `SetList` 方法，ASP 网页可以将值与 SNMP oid 数组关联起来。

<a name="syntax"></a>语法
------

```cpp
HRESULT SetList(
  [in] VARIANT *varName,
  [in] VARIANT *varValue
);
```

<a name="parameters"></a>参数
----------

*varName* \[中\]  
调用方提供的指向 SNMP OID 字符串的数组的指针。

*varValue* \[中\]  
调用方提供的指向 OID 值的数组的指针。

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

此方法调用 **SnmpMgrRequest** 函数来设置 SNMP OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

必须先调用 [**ISNMP：： Open**](isnmp-open.md) 方法，然后才能 `ISNMP::SetList` 调用方法。

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
