---
title: Iasphelp CalcJobETA 方法
description: 使用 CalcJobETA 方法，ASP 网页可以计算完成打印作业的时间。
MS-HAID:
- webfnc\_65577773-9d44-429e-a2fe-eb1a1475b7f6.xml
- print.iasphelp\_calcjobeta
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- CalcJobETA 方法打印设备
- CalcJobETA 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，CalcJobETA 方法
topic_type:
- apiref
api_name:
- Iasphelp.CalcJobETA
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3943da1dfe2782e5aa2a8892da220016ac352efc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835803"
---
# <a name="iasphelpcalcjobeta-method"></a>Iasphelp：： CalcJobETA 方法

使用 **CalcJobETA** 方法，ASP 网页可以计算完成打印作业的时间。

<a name="syntax"></a>语法
------

```cpp
HRESULT CalcJobETA();
```

<a name="parameters"></a>参数
----------

此方法没有任何参数。

<a name="return-value"></a>返回值
------------

下表显示此方法可能返回的值。

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
<td><p>方法成功。</p></td>
</tr>
<tr class="even">
<td><strong>E_HANDLE</strong></td>
<td><p>未调用 <strong>Iasphelp：： Open</strong> 方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

 

## <a name="vbscript-example"></a>VBScript 示例

**CalcJobETA** 方法计算可随后使用 Iasphelp 属性检索的打印作业信息。 获取以下任何属性之前，请先调用 **CalcJobETA** ：

[**Iasphelp::JobCompletionMinute**](iasphelp-jobcompletionminute.md)

[**Iasphelp：:P endingJobCount**](iasphelp-pendingjobcount.md)

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

在调用 **CalcJobETA** 之前，其中任何一个属性的值都为零。 如果 **CalcJobETA** 确定打印机速度不适用于当前打印机，则对 JobCompletionMinute 的后续调用将检索值-1。

必须先调用 [**Iasphelp：： Open**](iasphelp-open.md) 方法，然后才能调用 **CalcJobETA** 方法。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
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

[**Iasphelp::JobCompletionMinute**](iasphelp-jobcompletionminute.md)

[**Iasphelp：:P endingJobCount**](iasphelp-pendingjobcount.md)

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

[**Iasphelp：： Open**](iasphelp-open.md)
