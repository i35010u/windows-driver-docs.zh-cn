---
title: ISNMP Close 方法
description: Close 方法使 ASP Web 页面能够关闭到 SNMP 代理的通信路径。
MS-HAID:
- webfnc\_e925ae51-c717-4b4f-8ab2-b18e9d770c63.xml
- print.isnmp\_close
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 关闭方法打印设备
- 关闭方法打印设备，ISNMP 接口
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
ms.openlocfilehash: ae099adcdc673d5e990593877e07d9d082f74593
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796525"
---
# <a name="isnmpclose-method"></a>ISNMP：： Close 方法

使用 `Close` 方法，ASP 网页可以关闭到 SNMP 代理的通信路径。

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

方法始终返回 \_ "OK"。

## <a name="vbscript-example"></a>VBScript 示例

此方法调用 **SnmpMgrClose** 函数，该函数在 Windows SDK 文档中进行了介绍，用于关闭先前调用 [**ISNMP：： Open**](isnmp-open.md) 方法创建的通信路径。

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
