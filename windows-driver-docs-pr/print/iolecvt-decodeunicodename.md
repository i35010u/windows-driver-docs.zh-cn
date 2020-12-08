---
title: IOleCvt DecodeUnicodeName 方法
description: 使用 DecodeUnicodeName 属性，ASP 网页可以将 Unicode 字符串转换为其 ANSI 等效项。
MS-HAID:
- webfnc\_50fe9203-d31e-4af4-a34f-b32dfd3dd7b1.xml
- print.iolecvt\_decodeunicodename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: a7070737b48a45a0af484e099944dd8867fee9d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796651"
---
# <a name="iolecvtdecodeunicodename-method"></a>IOleCvt：:D ecodeUnicodeName 方法

使用 **DecodeUnicodeName** 属性，ASP 网页可以将 Unicode 字符串转换为其 ANSI 等效项。

<a name="syntax"></a>语法
------

```cpp
[propget, id(3), helpstring("property DecodeUnicodeName")] HRESULT DecodeUnicodeName(
  [in]          BSTR bstrSrcName,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrSrcName* \[中\]  
要转换的调用方提供的 Unicode 字符串。

*pVal* \[out，retval\]  
调用方提供的指向接收已翻译字符串的位置的指针。

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
<td><p>至少一个参数不指向有效的内存位置。</p></td>
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
<td>台式机</td>
</tr>
</tbody>
</table>
