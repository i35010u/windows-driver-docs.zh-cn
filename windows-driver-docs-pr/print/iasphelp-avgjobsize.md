---
title: Iasphelp get \_ AvgJobSize 方法
description: 使用 AvgJobSize 属性，ASP 网页可以确定打印作业的平均作业大小。
MS-HAID:
- webfnc\_de863905-eb8f-430a-a70b-7cb404dd3717.xml
- print.iasphelp\_avgjobsize
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_AvgJobSize 方法打印设备
- get_AvgJobSize 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_AvgJobSize 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_AvgJobSize
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00c3816bbf229f73418b75ab00889f916afa8dc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835811"
---
# <a name="iasphelpget_avgjobsize-method"></a>Iasphelp：： get \_ AvgJobSize 方法


使用 **AvgJobSize** 属性，ASP 网页可以确定打印作业的平均作业大小。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_AvgJobSize(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向接收平均作业大小的内存位置的指针。 有关此参数的详细信息，请参阅下面的 "备注" 部分。

<a name="return-value"></a>返回值
------------

成功时，此方法返回 S \_ OK。

## <a name="vbscript-example"></a>VBScript 示例

平均作业大小可以表示为每个作业的页数或每个作业的字节数。 使用 [**Iasphelp：： AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md) 属性来确定适用于 **Iasphelp：： AvgJobSize** 属性的单元。

在查询此属性之前，请调用 [**Iasphelp：： CalcJobETA**](iasphelp-calcjobeta.md) 方法来初始化属性值。

```vb
Dim objPrinter, strPrinter, JobSizeAvg
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
JobSizeAvg = objPrinter.AvgJobSize
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

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
