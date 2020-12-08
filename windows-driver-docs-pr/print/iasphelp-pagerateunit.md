---
title: Iasphelp get \_ PageRateUnit 方法
description: 使用 PageRateUnit，ASP 网页可以确定表示页面速率的单位。
MS-HAID:
- webfnc\_c3c557fb-2ce9-4260-838a-4bd0e56fb63d.xml
- print.iasphelp\_pagerateunit
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 909004dca49762061fbefae42adc243d919823cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835759"
---
# <a name="iasphelpget_pagerateunit-method"></a>Iasphelp：： get \_ PageRateUnit 方法

使用 **PageRateUnit** ，ASP 网页可以确定表示页面速率的单位。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PageRateUnit(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向内存位置的指针，该内存位置接收指示在页面速率中使用的单位的值。 下表显示了四个可能的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>打印速率单位为每分钟页数。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>每秒打印速率单位为个字符。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>每分钟打印速率单位数。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>每分钟打印速率单位为英寸。</p></td>
</tr>
</tbody>
</table>

这些值对应于 \_ \_ \_ \_ 在 Wingdi 标头文件中定义的常量 PRINTRATEUNIT PPM、PRINTRATEUNIT CPS、PRINTRATEUNIT LPM 和 PRINTRATEUNIT IPM。 有关这些常量的详细信息，请参阅 Windows SDK 文档中的 **DeviceCapabilities** 函数说明。

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

查询此属性，以确定表示 [**Iasphelp：:P agerate**](iasphelp-pagerate.md) 属性值的单位。

在查询 **Iasphelp：:P agerateunit** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：:P ageRate**](iasphelp-pagerate.md)

[**Iasphelp：： Open**](iasphelp-open.md)
