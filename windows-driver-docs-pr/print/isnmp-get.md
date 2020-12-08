---
title: ISNMP Get 方法
description: Get 方法使 ASP 网页能够获取由 SNMP OID 标识的值。
MS-HAID:
- webfnc\_e3167766-cd60-4ae7-9c06-9a1ccb5ac3b9.xml
- print.isnmp\_get
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 获取方法打印设备
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
ms.openlocfilehash: fd17239b9186e9be40ffd06a0049fa7146d53447
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835509"
---
# <a name="isnmpget-method"></a>ISNMP：： Get 方法

使用 `Get` 方法，ASP 网页可以获取由 SNMP OID 标识的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT Get(
  [in]  BSTR    bstrOID,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>参数
----------

*bstrOID* \[中\]  
调用方提供的 OID 字符串指针。

*varValue* \[弄\]  
调用方提供的用于接收 OID 值的位置。

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
<td><p>指定的 OID 无效。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法调用 **SnmpMgrRequest** 函数以获取 OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

必须先调用 [**ISNMP：： Open**](isnmp-open.md) 方法，然后才能 `ISNMP::Get` 调用方法。

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
