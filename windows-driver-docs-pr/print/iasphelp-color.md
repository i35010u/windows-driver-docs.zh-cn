---
title: Iasphelp get\_颜色方法
description: 颜色属性启用 ASP 网页，以确定是否打印机支持彩色打印。
MS-HAID:
- webfnc\_1eb57c03-7aa3-4acb-8a2c-3327a37e019d.xml
- print.iasphelp\_color
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: aa075ce7-15fd-4c24-b704-b7b240414d05
keywords:
- get_Color 方法打印设备
- get_Color 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_Color 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_Color
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1829772e2828e6289eca3b3e8fa2edfcd9a1a18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351245"
---
# <a name="iasphelpgetcolor-method"></a>Iasphelp::get\_颜色方法

**颜色**属性启用 ASP 网页，以确定是否打印机支持彩色打印。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Color(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供指向用于接收的位置 **，则返回 TRUE**若打印机支持彩色打印或**FALSE**如果不是。

<a name="return-value"></a>返回值
------------

此外可以返回 Win32 错误代码。

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
<td><p><strong>Iasphelp::Open</strong>尚未调用方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::Color**属性可以进行查询。

```vb
Dim objPrinter, HasColor
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
HasColor = objPrinter.Color
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
