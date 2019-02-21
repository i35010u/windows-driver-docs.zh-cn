---
title: IOleCvt ToUtf8 方法
description: ToUtf8 属性启用 ASP Web 页后，可以转换为 utf-8 格式的 Unicode 字符的字符串。
MS-HAID:
- webfnc\_b88265bd-9013-4c9b-abe2-00010d5b43c3.xml
- print.iolecvt\_toutf8
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1c20041f-b05d-4158-8838-650d25118c65
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
ms.openlocfilehash: 34ec2ff373d5e825d357314657cc37d99a76a2c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534255"
---
# <a name="iolecvttoutf8-method"></a>IOleCvt::ToUtf8 方法

**ToUtf8**属性启用 ASP Web 页后，可以转换为 utf-8 格式的 Unicode 字符的字符串。

<a name="syntax"></a>语法
------

```cpp
[propget, id(1), helpstring("property ToUtf8")] HRESULT ToUtf8(
  [in]          BSTR bstrUnicode,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrUnicode* \[in\]  
要转换为 utf-8 格式的调用方提供的字符串。

*pVal* \[out, retval\]  
调用方提供位置将接收转换后的字符串的指针。

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

Utf-8 是所有的字符 （Universal Multibyte Octet-Coded 字符集） UCS 的替代编码表示形式。 它可以用于传输通过通信系统假定 0x00 到 0x7F 范围内的各个八位字节将根据 ISO/IEC 4873，包括根据 ISO/IEC 2022 的 8 位结构控制功能一 C0 组定义的文本数据。

在以下示例中，函数**编写**返回一个字符串转换为 utf-8 格式提供的全局变量`bUTF8`是**TRUE**。 否则为**编写**返回未修改的字符串。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>
