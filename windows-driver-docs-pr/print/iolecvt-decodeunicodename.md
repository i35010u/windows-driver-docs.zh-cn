---
title: IOleCvt DecodeUnicodeName 方法
description: DecodeUnicodeName 属性启用 ASP Web 页后，可以转换为其等效的 ANSI 的 Unicode 字符串。
MS-HAID:
- webfnc\_50fe9203-d31e-4af4-a34f-b32dfd3dd7b1.xml
- print.iolecvt\_decodeunicodename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: d00fdabd-611a-4f26-8ca5-21ba8c28d993
keywords:
- DecodeUnicodeName 方法打印设备
- DecodeUnicodeName 方法打印设备，IOleCvt 接口
- IOleCvt 接口打印设备，DecodeUnicodeName 方法
topic_type:
- apiref
api_name:
- IOleCvt.DecodeUnicodeName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f585b640594a8737272f7238c1a3c3428b3d69d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525349"
---
# <a name="iolecvtdecodeunicodename-method"></a>IOleCvt::DecodeUnicodeName 方法

**DecodeUnicodeName**属性启用 ASP Web 页后，可以转换为其 ANSI 等效的 Unicode 字符串。

<a name="syntax"></a>语法
------

```cpp
[propget, id(3), helpstring("property DecodeUnicodeName")] HRESULT DecodeUnicodeName(
  [in]          BSTR bstrSrcName,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrSrcName* \[in\]  
调用方提供 Unicode 字符串转换。

*pVal* \[out, retval\]  
调用方提供指向用于接收已转换的字符串的位置。

<a name="return-value"></a>返回值
------------

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
<td><strong>E_POINTER</strong></td>
<td><p>在至少一个参数不指向有效内存位置。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

```vb
Dim OleCvt, strPrinter, strEncodedPrinter
Set OleCvt = Server.CreateObject("OlePrn.OleCvt")
strEncodedPrinter = Request ( "eprinter" )
strPrinter = OleCvt.DecodeUnicodeName (strEncodedPrinter)
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
