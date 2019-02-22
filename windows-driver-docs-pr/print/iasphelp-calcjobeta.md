---
title: Iasphelp CalcJobETA 方法
description: CalcJobETA 方法启用 ASP 网页，若要计算的打印作业的完成的时间。
MS-HAID:
- webfnc\_65577773-9d44-429e-a2fe-eb1a1475b7f6.xml
- print.iasphelp\_calcjobeta
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: cdf4d590-c236-4ed7-a071-fd0ddbb78590
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
ms.openlocfilehash: de81d764a826b987923bbdb0c980725ec8f45d3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554692"
---
# <a name="iasphelpcalcjobeta-method"></a>Iasphelp::CalcJobETA 方法

**CalcJobETA**方法启用 ASP 网页，若要计算的打印作业的完成的时间。

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

下表显示了可能的此方法返回值。

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
<td><p><strong>Iasphelp::Open</strong>尚未调用方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

 

## <a name="vbscript-example"></a>VBScript 示例

**CalcJobETA**方法计算可以在使用 Iasphelp 属性随后检索的打印作业信息。 调用**CalcJobETA**之前遇到了任何以下属性：

[**Iasphelp::JobCompletionMinute**](iasphelp-jobcompletionminute.md)

[**Iasphelp::PendingJobCount**](iasphelp-pendingjobcount.md)

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

之前**CalcJobETA**是调用，任何这些属性的值为零。 如果**CalcJobETA**确定打印机速率不是可用于当前打印机、 JobCompletionMinute 的后续调用中检索的值为-1。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**CalcJobETA**可以调用方法。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp::JobCompletionMinute**](iasphelp-jobcompletionminute.md)

[**Iasphelp::PendingJobCount**](iasphelp-pendingjobcount.md)

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

[**Iasphelp::Open**](iasphelp-open.md)
