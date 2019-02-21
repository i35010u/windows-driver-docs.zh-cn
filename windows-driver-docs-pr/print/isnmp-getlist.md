---
title: ISNMP GetList 方法
description: GetList 方法，ASP 网页，以获得与数组 SNMP Oid 关联的值。
MS-HAID:
- webfnc\_44ada708-01e2-42c3-8080-bd7cf0e46b0e.xml
- print.isnmp\_getlist
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 6ee90c77-578e-4c2c-b955-4b549625ca14
keywords:
- GetList 方法打印设备
- GetList 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，GetList 方法
topic_type:
- apiref
api_name:
- ISNMP.GetList
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0005ceda8efe8fa4fa8d47c2b2e80a0395c0ed7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532994"
---
# <a name="isnmpgetlist-method"></a>ISNMP::GetList 方法

`GetList`方法启用 ASP 网页，以获得与数组 SNMP Oid 关联的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT GetList(
  [in]  VARIANT *varList,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>参数
----------

*varList* \[in\]  
调用方提供的 SNMP OID 字符串数组指针。

*varValue* \[out\]  
调用方提供的位置接收的 SNMP OID 值数组的地址的指针。

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

此方法调用**SnmpMgrRequest**函数获取 SNMP OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

[ **ISNMP::Open** ](isnmp-open.md)前必须调用方法`ISNMP::GetList`可以调用方法。

```vb
Dim StrIP, strCommunity, objSNMP, OIDArray, OIDValueArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDArray = Array("25.3.2.1.5", "25.3.5.1.1")
OIDValueArray = objSNMP.GetList (OIDArray)
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
