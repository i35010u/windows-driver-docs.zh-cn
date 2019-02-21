---
title: Iasphelp get\_PendingJobCount 方法
description: PendingJobCount 属性启用 ASP 网页来确定挂起的打印作业的数目。
MS-HAID:
- webfnc\_fd1cbaac-f195-4a38-8788-990eb9b3fd6c.xml
- print.iasphelp\_pendingjobcount
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e0d00abd-0b2a-403c-a7b2-f1f2587b977f
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
ms.openlocfilehash: 7c7f5efc765e7422e0700169211963424b0ca8e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555337"
---
# <a name="iasphelpgetpendingjobcount-method"></a>Iasphelp::get\_PendingJobCount 方法

**PendingJobCount**属性启用 ASP 网页来确定挂起的打印作业的数目。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PendingJobCount(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
指向接收挂起的打印作业的数量的内存位置的调用方提供的指针。

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

查询此属性之前，调用[ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)方法来初始化的属性值。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp::Open**](iasphelp-open.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
