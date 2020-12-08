---
title: ISNMP OIDFromString 方法
description: 使用 OIDFromString 方法，ASP 网页可以将 SNMP OID 字符串转换为数字数组。
MS-HAID:
- webfnc\_de08026f-5b6b-4c82-a653-2e16606e6b85.xml
- print.isnmp\_oidfromstring
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- OIDFromString 方法打印设备
- OIDFromString 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，OIDFromString 方法
topic_type:
- apiref
api_name:
- ISNMP.OIDFromString
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1f45c28a493ee3425613f475560d284b6f7b54f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796511"
---
# <a name="isnmpoidfromstring-method"></a>ISNMP：： OIDFromString 方法

使用 `OIDFromString` 方法，ASP 网页可以将 SNMP OID 字符串转换为数字数组。

<a name="syntax"></a>语法
------

```cpp
HRESULT OIDFromString(
  [in]  BSTR    bstrOID,
  [out] VARIANT *varOID
);
```

<a name="parameters"></a>参数
----------

*bstrOID* \[中\]  
调用方提供的指向 SNMP OID 字符串的指针。

*varOID* \[弄\]  
调用方提供的位置，用于接收指向表示 SNMP OID 的整数值数组的指针。

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
<td><strong>E_INVALIDARG</strong></td>
<td><p>指定的 SNMP OID 无效。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法调用 **SnmpMgrStrToOid** 函数，将 SNMP OID 字符串转换为其对应的内部对象标识符结构。 有关此函数的详细信息，请参阅 Windows SDK 文档。

```vb
Dim StrIP, strCommunity, objSNMP, OIDArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDArray = objSNMP.OIDFromString (". 43.18.1.1.2")
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
