---
title: Iasphelp get\_PageRateUnit 方法
description: PageRateUnit 启用 ASP 网页，以确定分页速率表示的单位。
MS-HAID:
- webfnc\_c3c557fb-2ce9-4260-838a-4bd0e56fb63d.xml
- print.iasphelp\_pagerateunit
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1b528527-a03a-4fab-b118-5c744759a0a1
keywords:
- get_PageRateUnit 方法打印设备
- get_PageRateUnit 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_PageRateUnit 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_PageRateUnit
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acbf199ce49bb180b2640134d7e8f09c46be1fab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555388"
---
# <a name="iasphelpgetpagerateunit-method"></a>Iasphelp::get\_PageRateUnit 方法

**PageRateUnit**启用 ASP 网页，以确定分页速率表示的单位。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PageRateUnit(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
指向接收值，该值指示页速率中使用的单位的内存位置的调用方提供的指针。 下表中显示四个可能的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>打印速度单位为每分钟页数。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>打印速度单位为每秒的字符。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>打印速度单位为每分钟的行。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>打印速度单位为每分钟英寸为单位。</p></td>
</tr>
</tbody>
</table>

这些值对应于常量 PRINTRATEUNIT\_PPM、 PRINTRATEUNIT\_CPS、 PRINTRATEUNIT\_LPM 和 PRINTRATEUNIT\_IPM，Wingdi.h 标头文件中定义。 有关这些常量的详细信息，请参阅的说明**DeviceCapabilities** Windows SDK 文档中的函数。

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

通过查询此属性来确定的单位[ **Iasphelp::PageRate** ](iasphelp-pagerate.md)表示属性值。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::PageRateUnit**属性可以进行查询。

```vb
Dim objPrinter, PtrPageRateUnit
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrPageRate = objPrinter.PageRateUnit
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

## <a name="see-also"></a>另请参阅

[**Iasphelp::PageRate**](iasphelp-pagerate.md)

[**Iasphelp::Open**](iasphelp-open.md)
