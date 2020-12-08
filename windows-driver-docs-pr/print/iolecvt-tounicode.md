---
title: IOleCvt ToUnicode 方法
description: 使用 ToUnicode 属性，ASP 网页可以使用指定的代码页将一个 Unicode 字符串转换为另一个 Unicode 字符串。
MS-HAID:
- webfnc\_37f4684f-4af9-4e25-8c5e-6ad63748cf5d.xml
- print.iolecvt\_tounicode
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- ToUnicode 方法打印设备
- ToUnicode 方法打印设备，IOleCvt 接口
- IOleCvt 接口打印设备，ToUnicode 方法
topic_type:
- apiref
api_name:
- IOleCvt.ToUnicode
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686bef53b04a862252dae0d5c78bb93b2da1ea31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835603"
---
# <a name="iolecvttounicode-method"></a>IOleCvt：： ToUnicode 方法

使用 **ToUnicode** 属性，ASP 网页可以使用指定的代码页将一个 Unicode 字符串转换为另一个 Unicode 字符串。

<a name="syntax"></a>语法
------

```cpp
[propget, id(4), helpstring("property ToUnicode")] HRESULT ToUnicode(
  [in]          BSTR bstrString,
  [in]          Long lCodePage,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrString* \[中\]  
调用方提供的要转换的字符串。

*lCodePage* \[中\]  
调用方提供的用于转换的代码页。 有关更多信息，请参见下面的“备注”部分。

*pVal* \[out，retval\]  
调用方提供的指向接收转换的 Unicode 字符串的位置的指针。

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

<a name="remarks"></a>备注
-------

将 *lCodePage* 参数设置为为 **MultiByteToWideChar** 函数 *的代码页参数定义* 的代码页标识符之一。 有关此函数的详细信息，请参阅 Windows SDK 文档。

尽管大多数应用程序现在使用 Unicode (字符数据的 UTF-16) 编码，但某些 Windows 桌面应用程序使用基于 Windows 代码页的字符集。 代码页将国际字符分配到大于127的 ANSI 字符代码。 有关代码页的详细信息，请参阅 Windows SDK 文档。

使用日语代码页转换为 Unicode （如果适用）。

```vb
If strLang = "JP" Then
    tmpStr = OleCvt.ToUnicode (str, 932)
Else
    tmpStr = str
End If
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
