---
title: IOleCvt ToUnicode 方法
description: ToUnicode 属性启用 ASP Web 页后，可以将一个 Unicode 字符串转换为另一个使用指定的代码页。
MS-HAID:
- webfnc\_37f4684f-4af9-4e25-8c5e-6ad63748cf5d.xml
- print.iolecvt\_tounicode
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e03997f6-e9b5-403e-99da-52504960cb99
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
ms.openlocfilehash: d65d923424f33bc48dc3201f46c4cda11266ab94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324858"
---
# <a name="iolecvttounicode-method"></a>IOleCvt::ToUnicode 方法

**ToUnicode**属性启用 ASP 网页，将一个 Unicode 字符串转换为另一个使用指定的代码页。

<a name="syntax"></a>语法
------

```cpp
[propget, id(4), helpstring("property ToUnicode")] HRESULT ToUnicode(
  [in]          BSTR bstrString,
  [in]          Long lCodePage,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>Parameters
----------

*bstrString* \[in\]  
要转换的调用方提供的字符串。

*lCodePage* \[in\]  
若要使用用于转换的调用方提供的代码页。 有关详细信息，请参阅以下备注部分。

*pVal* \[out, retval\]  
调用方提供的位置以接收转换后的 Unicode 字符串指针。

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

<a name="remarks"></a>备注
-------

设置*lCodePage*参数为定义的代码页标识符之一*代码页*参数**MultiByteToWideChar**函数。 有关此函数的详细信息，请参阅 Windows SDK 文档。

尽管大多数应用程序现在使用 Unicode (utf-16) 编码为字符数据，但某些 Windows 桌面应用程序使用基于 Windows 代码页的字符集。 代码页将国际字符分配给大于 127 的 ANSI 字符代码。 有关代码页的详细信息，请参阅 Windows SDK 文档。

如果适用，将转换为 Unicode 使用日语代码页。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>
