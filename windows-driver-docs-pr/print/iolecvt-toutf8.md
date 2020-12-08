---
title: IOleCvt ToUtf8 方法
description: 使用 ToUtf8 属性，ASP 网页可以将 Unicode 字符的字符串转换为 UTF-8 格式。
MS-HAID:
- webfnc\_b88265bd-9013-4c9b-abe2-00010d5b43c3.xml
- print.iolecvt\_toutf8
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- ToUtf8 方法打印设备
- ToUtf8 方法打印设备，IOleCvt 接口
- IOleCvt 接口打印设备，ToUtf8 方法
topic_type:
- apiref
api_name:
- IOleCvt.ToUtf8
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e430377192ced1492a8eac36d878d78dd8b992
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796645"
---
# <a name="iolecvttoutf8-method"></a>IOleCvt：： ToUtf8 方法

使用 **ToUtf8** 属性，ASP 网页可以将 Unicode 字符的字符串转换为 utf-8 格式。

<a name="syntax"></a>语法
------

```cpp
[propget, id(1), helpstring("property ToUtf8")] HRESULT ToUtf8(
  [in]          BSTR bstrUnicode,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrUnicode* \[中\]  
调用方提供的字符串，用于转换为 UTF-8 格式。

*pVal* \[out，retval\]  
调用方提供的指向将接收转换后的字符串的位置的指针。

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

UTF-8 是一种替代编码表示形式，适用于 UCS (通用多字节 Octet-Coded 字符集) 的所有字符。 它可用于通过通信系统传输文本数据，这假定从0x00 到0x7F 的范围内的单个八位字节具有根据 ISO/IEC 4873 定义的定义，其中包括根据 ISO/IEC 2022 的8位结构控制功能。

在下面的示例中，函数 **Write** 返回转换为 utf-8 格式的字符串，前提是全局变量 `bUTF8` 为 **TRUE**。 否则， **Write** 将返回未修改的字符串。

```vb
Function Write (strUnicode)
    If bUTF8 Then
        Write = OleCvt.ToUtf8 (strUnicode)
    Else
        Write = strUnicode
    End If
End Function
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
