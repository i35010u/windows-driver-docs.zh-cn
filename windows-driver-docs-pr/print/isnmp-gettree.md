---
title: ISNMP GetTree 方法
description: GetTree 方法启用 ASP 网页，以获得与指定的 SNMP OID 根下的子节点的一组相关联的值。
MS-HAID:
- webfnc\_bb1a8a21-716c-41ab-8b88-5f26d19575fa.xml
- print.isnmp\_gettree
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: a58cc911-dc09-4847-b4b7-cf97326cd444
keywords:
- GetTree 方法打印设备
- GetTree 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，GetTree 方法
topic_type:
- apiref
api_name:
- ISNMP.GetTree
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 902fb78760f48d5f928495146f776caf90acef7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384185"
---
# <a name="isnmpgettree-method"></a>ISNMP::GetTree 方法

`GetTree`方法启用 ASP 网页，以获得与指定的 SNMP OID 根下的子节点的一组相关联的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT GetTree(
  [in]  BSTR    varTree,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>Parameters
----------

*varTree* \[in\]  
标识根 SNMP OID 的调用方提供的字符串。

*varValue* \[out\]  
接收包含 SNMP OID 字符串和关联的值的二维数组的地址的调用方提供的位置。

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

此方法调用**SnmpMgrRequest**函数获取 SNMP OID 子节点的值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

[ **ISNMP::Open** ](isnmp-open.md)前必须调用方法`ISNMP::GetTree`可以调用方法。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValueArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDValueArray = objSNMP.GetTree ("43.18.1.1.2")
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
