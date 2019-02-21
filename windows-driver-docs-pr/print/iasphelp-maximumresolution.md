---
title: Iasphelp get\_MaximumResolution 方法
description: MaximumResolution 属性启用 ASP 网页，以确定打印机的最大分辨率。
MS-HAID:
- webfnc\_156e8337-489a-44e6-9c81-0a8f6dd3aa08.xml
- print.iasphelp\_maximumresolution
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 74dffe85-0e6d-4c2c-a933-2afb68624c76
keywords:
- get_MaximumResolution 方法打印设备
- get_MaximumResolution 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_MaximumResolution 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_MaximumResolution
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c9d90063a67bbbc9003780781ad6af5b6108f31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526708"
---
# <a name="iasphelpgetmaximumresolution-method"></a>Iasphelp::get\_MaximumResolution 方法

**MaximumResolution**属性启用 ASP 网页，以确定打印机的最大分辨率。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_MaximumResolution(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
要接收一个数值表示打印机的最大分辨率，以每英寸点数的调用方提供的位置。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::MaximumResolution**属性可以进行查询。

```vb
Dim objPrinter, MaxRes
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
MaxRes = objPrinter.MaximumResolution
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
