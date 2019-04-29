---
title: Iasphelp get\_AvgJobSizeUnit 方法
description: AvgJobSizeUnit 属性启用 ASP 网页，以确定平均作业大小的单位。
MS-HAID:
- webfnc\_b7542526-ad13-46d7-a1c1-e02d7832dfb6.xml
- print.iasphelp\_avgjobsizeunit
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: f5a701ff-270f-45f5-8c6e-ecf1b8afab20
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
ms.openlocfilehash: 63320ba94707ed0990adf15b59af555a901ab844
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361859"
---
# <a name="iasphelpgetavgjobsizeunit-method"></a>Iasphelp::get\_AvgJobSizeUnit 方法


**AvgJobSizeUnit**属性启用 ASP 网页，以确定平均作业大小的单位。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_AvgJobSizeUnit(
  [out] long *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
指向接收的值之一下表中的内存位置的调用方提供的指针。 值指示所带来的平均作业大小的单位。

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
<td><p>平均作业大小的单位为每个作业页中。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>平均作业大小的单位是以字节为单位，每个作业。</p></td>
</tr>
</tbody>
</table>

 

<a name="return-value"></a>返回值
------------

此方法返回时 S\_成功的确定。

## <a name="vbscript-example"></a>VBScript 示例

查询**Iasphelp::AvgJobSizeUnit**属性来确定的单位[ **Iasphelp::AvgJobSize** ](iasphelp-avgjobsize.md)表示属性值。

查询此属性之前，调用[ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)方法来初始化的属性值。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
