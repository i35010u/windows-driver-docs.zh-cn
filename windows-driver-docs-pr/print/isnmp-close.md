---
title: ISNMP Close 方法
description: Close 方法启用 ASP 网页，以关闭到 SNMP 代理的通信路径。
MS-HAID:
- webfnc\_e925ae51-c717-4b4f-8ab2-b18e9d770c63.xml
- print.isnmp\_close
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ea3c462d-881d-48ad-8751-d3ee0468697e
keywords:
- Close 方法打印设备
- Close 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，Close 方法
topic_type:
- apiref
api_name:
- ISNMP.Close
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19d980f4b1d98cc90c17f5e179e5ea42e625e804
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520113"
---
# <a name="isnmpclose-method"></a>ISNMP::Close 方法

`Close`方法启用 ASP 网页，以关闭到 SNMP 代理的通信路径。

<a name="syntax"></a>语法
------

```cpp
HRESULT Close();
```

<a name="parameters"></a>参数
----------

此方法没有任何参数。

<a name="return-value"></a>返回值
------------

该方法始终返回 S\_确定。

## <a name="vbscript-example"></a>VBScript 示例

此方法调用**SnmpMgrClose**函数，Windows SDK 文档，以关闭已通过以前调用的通信路径中所述[ **ISNMP::Open**](isnmp-open.md)方法。

```vb
Dim StrIP, strCommunity, objSNMP
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
...
objSNMP.Close
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
