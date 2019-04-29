---
title: Iasphelp get\_AvgJobSize 方法
description: AvgJobSize 属性启用 ASP 网页，以确定序列中的打印作业的平均作业的大小。
MS-HAID:
- webfnc\_de863905-eb8f-430a-a70b-7cb404dd3717.xml
- print.iasphelp\_avgjobsize
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 3373376f-c904-47dd-8502-c2c26caed3be
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
ms.openlocfilehash: 47fac5c86d5b2602ef173eb9582ea8e9b4b73a69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361736"
---
# <a name="iasphelpgetavgjobsize-method"></a>Iasphelp::get\_AvgJobSize 方法


**AvgJobSize**属性启用 ASP 网页，以确定序列中的打印作业的平均作业的大小。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_AvgJobSize(
  [out] long *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
指向接收的平均作业大小的内存位置的调用方提供的指针。 有关此参数的详细信息，请参阅以下备注部分。

<a name="return-value"></a>返回值
------------

此方法返回时 S\_成功的确定。

## <a name="vbscript-example"></a>VBScript 示例

可以为每个作业的页面数或每个作业的字节数表示的平均作业的大小。 使用[ **Iasphelp::AvgJobSizeUnit** ](iasphelp-avgjobsizeunit.md)属性来确定哪些单元适用于**Iasphelp::AvgJobSize**属性。

查询此属性之前，调用[ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)方法来初始化的属性值。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
