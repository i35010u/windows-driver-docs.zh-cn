---
title: Iasphelp get\_JobCompletionMinute 方法
description: JobCompletionMinute 属性启用 ASP 网页，以确定何时将完成当前处于挂起状态的打印作业。
MS-HAID:
- webfnc\_63bca3eb-0ead-4430-8e82-9014d58c133b.xml
- print.iasphelp\_jobcompletionminute
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e3dba870-84b4-4959-8ed4-102ac82be14b
keywords:
- get_JobCompletionMinute 方法打印设备
- get_JobCompletionMinute 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_JobCompletionMinute 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_JobCompletionMinute
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c50ccdeb1454a184cfaac36460a0f9fb6bfed3ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392833"
---
# <a name="iasphelpgetjobcompletionminute-method"></a>Iasphelp::get\_JobCompletionMinute 方法

**JobCompletionMinute**属性启用 ASP 网页，以确定何时将完成当前处于挂起状态的打印作业。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_JobCompletionMinute(
  [out] long *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
指向接收所需的时间，以分钟为单位，对所有打印作业正在等待完成的内存位置的调用方提供的指针。

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

查询此属性之前，调用[ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)方法来初始化的属性值。 若要确定的挂起的打印作业的数目，请查询[ **Iasphelp::PendingJobCount** ](iasphelp-pendingjobcount.md)属性。

```vb
Dim objPrinter, EndMinute
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
EndMinute = objPrinter.JobCompletionMinute
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

[**Iasphelp::Open**](iasphelp-open.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)

[**Iasphelp::PendingJobCount**](iasphelp-pendingjobcount.md)
