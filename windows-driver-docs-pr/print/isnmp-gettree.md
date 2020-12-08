---
title: ISNMP GetTree 方法
description: 使用 GetTree 方法可以获取与指定的根 SNMP OID 下的一组子节点相关联的值。
MS-HAID:
- webfnc\_bb1a8a21-716c-41ab-8b88-5f26d19575fa.xml
- print.isnmp\_gettree
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 3873639d32064704b0ea1c4fa322888a841a2275
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796514"
---
# <a name="isnmpgettree-method"></a>ISNMP：： GetTree 方法

使用 `GetTree` 方法，ASP 网页可以获取与指定的根 SNMP OID 下的一组子节点相关联的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT GetTree(
  [in]  BSTR    varTree,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>参数
----------

*varTree* \[中\]  
调用方提供的用于标识根 SNMP OID 的字符串。

*varValue* \[弄\]  
调用方提供的位置，用于接收包含 SNMP OID 字符串和关联值的二维数组的地址。

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

此方法调用 **SnmpMgrRequest** 函数以获取子节点的 SNMP OID 值。 有关此函数的详细信息，请参阅 Windows SDK 文档。

必须先调用 [**ISNMP：： Open**](isnmp-open.md) 方法，然后才能 `ISNMP::GetTree` 调用方法。

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
