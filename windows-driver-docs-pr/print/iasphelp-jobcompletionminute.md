---
title: Iasphelp get \_ JobCompletionMinute 方法
description: 使用 JobCompletionMinute 属性，ASP 网页可以确定当前挂起的打印作业何时完成。
MS-HAID:
- webfnc\_63bca3eb-0ead-4430-8e82-9014d58c133b.xml
- print.iasphelp\_jobcompletionminute
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: d1c19a60dec3ec5e693a48706a8016ea2eb06707
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835775"
---
# <a name="iasphelpget_jobcompletionminute-method"></a>Iasphelp：： get \_ JobCompletionMinute 方法

使用 **JobCompletionMinute** 属性，ASP 网页可以确定当前挂起的打印作业何时完成。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_JobCompletionMinute(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向内存位置的指针，该指针接收当前挂起完成的所有打印作业所需的时间（以分钟为单位）。

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

在查询此属性之前，请调用 [**Iasphelp：： CalcJobETA**](iasphelp-calcjobeta.md) 方法来初始化属性值。 若要确定挂起的打印作业数，请查询 [**Iasphelp：:P endingjobcount**](iasphelp-pendingjobcount.md) 属性。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)

[**Iasphelp：:P endingJobCount**](iasphelp-pendingjobcount.md)
