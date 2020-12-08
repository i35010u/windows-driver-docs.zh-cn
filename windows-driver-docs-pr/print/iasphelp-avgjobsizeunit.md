---
title: Iasphelp get \_ AvgJobSizeUnit 方法
description: 使用 AvgJobSizeUnit 属性，ASP 网页可以确定平均作业大小的单位。
MS-HAID:
- webfnc\_b7542526-ad13-46d7-a1c1-e02d7832dfb6.xml
- print.iasphelp\_avgjobsizeunit
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_AvgJobSizeUnit 方法打印设备
- get_AvgJobSizeUnit 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_AvgJobSizeUnit 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_AvgJobSizeUnit
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26863461e65f8b54d2b7067451c2d95e5c245447
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796837"
---
# <a name="iasphelpget_avgjobsizeunit-method"></a>Iasphelp：： get \_ AvgJobSizeUnit 方法


使用 **AvgJobSizeUnit** 属性，ASP 网页可以确定平均作业大小的单位。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_AvgJobSizeUnit(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向内存位置的指针，该内存位置接收下表中的值之一。 值指示与平均作业大小关联的单位。

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
<td><p>每个作业的平均作业大小单位为个页面。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>每个作业的平均作业大小单位数（以字节为单位）。</p></td>
</tr>
</tbody>
</table>

 

<a name="return-value"></a>返回值
------------

成功时，此方法返回 S \_ OK。

## <a name="vbscript-example"></a>VBScript 示例

查询 **Iasphelp：： AvgJobSizeUnit** 属性以确定表示 [**Iasphelp：： AvgJobSize**](iasphelp-avgjobsize.md) 属性值的单位。

在查询此属性之前，请调用 [**Iasphelp：： CalcJobETA**](iasphelp-calcjobeta.md) 方法来初始化属性值。

```vb
Dim objPrinter, strPrinter, JobUnits
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
JobUnits = objPrinter.AvgJobSizeUnit
' If JobUnits = 1 then job size is in units of pages
' If JobUnits = 2 then job size is in units of bytes
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

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
