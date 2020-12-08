---
title: ISNMP 执行 getlist 方法
description: 使用执行 getlist 方法可以获取与 SNMP Oid 数组相关联的值。
MS-HAID:
- webfnc\_44ada708-01e2-42c3-8080-bd7cf0e46b0e.xml
- print.isnmp\_getlist
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 执行 getlist 方法打印设备
- 执行 getlist 方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，执行 getlist 方法
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
ms.openlocfilehash: 494938b6e521da584bca517d93369c6c8b25aefe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835507"
---
# <a name="isnmpgetlist-method"></a>ISNMP：：执行 getlist 方法

`GetList`方法使 ASP 网页能够获取与 SNMP oid 数组关联的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT GetList(
  [in]  VARIANT *varList,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>参数
----------

*varList* \[中\]  
调用方提供的指向 SNMP OID 字符串的数组的指针。

*varValue* \[弄\]  
调用方提供的指向接收 SNMP OID 值数组地址的位置的指针。

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

此方法调用 **SnmpMgrRequest** 函数以获取 SNMP OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

必须先调用 [**ISNMP：： Open**](isnmp-open.md) 方法，然后才能 `ISNMP::GetList` 调用方法。

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
