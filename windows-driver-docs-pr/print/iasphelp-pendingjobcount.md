---
title: Iasphelp get \_ PendingJobCount 方法
description: 使用 PendingJobCount 属性可以确定挂起的打印作业的数目。
MS-HAID:
- webfnc\_fd1cbaac-f195-4a38-8788-990eb9b3fd6c.xml
- print.iasphelp\_pendingjobcount
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_PendingJobCount 方法打印设备
- get_PendingJobCount 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_PendingJobCount 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_PendingJobCount
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87bc56f35520698a70740edddf21d0e37bd1f09e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835757"
---
# <a name="iasphelpget_pendingjobcount-method"></a>Iasphelp：： get \_ PendingJobCount 方法

使用 **PendingJobCount** 属性可以确定挂起的打印作业的数目。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PendingJobCount(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向内存位置的指针，该内存位置接收挂起的打印作业的数目。

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

在查询此属性之前，请调用 [**Iasphelp：： CalcJobETA**](iasphelp-calcjobeta.md) 方法来初始化属性值。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
PendingJobs = objPrinter.PendingJobCount
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
