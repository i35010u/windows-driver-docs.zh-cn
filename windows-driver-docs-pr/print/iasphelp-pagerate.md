---
title: Iasphelp get \_ PageRate 方法
description: 使用 PageRate 属性可以使 ASP 网页确定打印机的页面速度。
MS-HAID:
- webfnc\_f356953e-ac15-4948-9a6e-b83d3aec8e7b.xml
- print.iasphelp\_pagerate
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_PageRate 方法打印设备
- get_PageRate 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_PageRate 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_PageRate
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d839dead4385eefd5887ca198aa7def1740750
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796797"
---
# <a name="iasphelpget_pagerate-method"></a>Iasphelp：： get \_ PageRate 方法

使用 **PageRate** 属性可以使 ASP 网页确定打印机的页面速度。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PageRate(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的位置，用于接收表示打印机的页面速率的数字值。 表示页面速率的单位可能取决于打印机。 有关页面速度的详细信息，请参阅下面的 "备注" 部分。

<a name="return-value"></a>返回值
------------

此属性返回下表中的值之一。

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
<td><strong>E_HANDLE</strong></td>
<td><p>未调用 <a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"><strong>Iasphelp：： Open</strong></a> 方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例


若要确定测量页面速率的单位，请查询 [**Iasphelp：:P agerateunit**](iasphelp-pagerateunit.md) 属性。

在查询 **Iasphelp：:P agerate** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, PtrPageRate
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrPageRate = objPrinter.PageRate
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
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：:P ageRateUnit**](iasphelp-pagerateunit.md)

[**Iasphelp：： Open**](iasphelp-open.md)
