---
title: ISNMP Get 方法
description: Get 方法启用 ASP 网页，以获取标识 SNMP OID 的值。
MS-HAID:
- webfnc\_e3167766-cd60-4ae7-9c06-9a1ccb5ac3b9.xml
- print.isnmp\_get
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 0cecdc34-63d9-46da-ba4e-a44780f5bb25
keywords:
- Get 方法打印设备
- 获取方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，Get 方法
topic_type:
- apiref
api_name:
- ISNMP.Get
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e938b7782787e61f2b741848e54a00da6e0a1892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562069"
---
# <a name="isnmpget-method"></a>ISNMP::Get 方法

`Get`方法启用 ASP 网页，以获取标识 SNMP OID 的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT Get(
  [in]  BSTR    bstrOID,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrOID* \[in\]  
调用方提供指向 OID 字符串指针。

*varValue* \[out\]  
要接收的 OID 值的调用方提供的位置。

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
<td><p>指定的 OID 无效。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法调用**SnmpMgrRequest**函数获取的 OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

[ **ISNMP::Open** ](isnmp-open.md)前必须调用方法`ISNMP::Get`可以调用方法。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValue
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDValue = objSNMP.Get ("43.18.1.1.2")
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
