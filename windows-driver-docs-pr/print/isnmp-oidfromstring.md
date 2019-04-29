---
title: ISNMP OIDFromString 方法
description: OIDFromString 方法启用 ASP 网页，若要将 SNMP OID 字符串转换为数值数组。
MS-HAID:
- webfnc\_de08026f-5b6b-4c82-a653-2e16606e6b85.xml
- print.isnmp\_oidfromstring
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: a0e12657-c34e-4aff-a068-911a6aa6959d
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
ms.openlocfilehash: 1458d9820f7bc2766c8f07f74b982d1b5d6a6fa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384183"
---
# <a name="isnmpoidfromstring-method"></a>ISNMP::OIDFromString 方法

`OIDFromString`方法启用 ASP 网页，若要将 SNMP OID 字符串转换为数值数组。

<a name="syntax"></a>语法
------

```cpp
HRESULT OIDFromString(
  [in]  BSTR    bstrOID,
  [out] VARIANT *varOID
);
```

<a name="parameters"></a>Parameters
----------

*bstrOID* \[in\]  
调用方提供指向 SNMP OID 字符串指针。

*varOID* \[out\]  
要接收指向一个整数值表示 SNMP OID 数组的指针的调用方提供的位置。

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

此方法调用**SnmpMgrStrToOid**函数将 SNMP OID 字符串转换为其相应的内部对象标识符结构。 有关此函数的详细信息，请参阅 Windows SDK 文档。

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
<td>桌面设备</td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Olesnmp.h</td>
</tr>
</tbody>
</table>
