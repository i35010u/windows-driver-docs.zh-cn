---
title: Iasphelp get\_PageRate 方法
description: PageRate 属性启用 ASP 网页，以确定打印机的分页速率。
MS-HAID:
- webfnc\_f356953e-ac15-4948-9a6e-b83d3aec8e7b.xml
- print.iasphelp\_pagerate
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 010f4871-f64f-465f-a78b-a86f91a9f194
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
ms.openlocfilehash: d3bff7d93b6a3d3ddea2f937fbd4f0f39fd2efb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564500"
---
# <a name="iasphelpgetpagerate-method"></a>Iasphelp::get\_PageRate 方法

**PageRate**属性启用 ASP 网页，以确定打印机的分页速率。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PageRate(
  [out] long *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供的位置，以接收表示打印机的页面速率的数字值。 表示页速率的单位可能取决于打印机。 有关页费率的详细信息，请参阅以下备注部分。

<a name="return-value"></a>返回值
------------

下表中，此属性返回的值之一。

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
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>尚未调用方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例


若要确定分页速率测量中的单元，请查询[ **Iasphelp::PageRateUnit** ](iasphelp-pagerateunit.md)属性。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::PageRate**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::PageRateUnit**](iasphelp-pagerateunit.md)

[**Iasphelp::Open**](iasphelp-open.md)
