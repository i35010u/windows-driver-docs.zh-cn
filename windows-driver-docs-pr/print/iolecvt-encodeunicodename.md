---
title: IOleCvt EncodeUnicodeName 方法
description: EncodeUnicodeName 属性启用 ASP Web 页后，可以转换为其等效的 Unicode 的 ANSI 字符串。
MS-HAID:
- webfnc\_e31e8dae-76bb-4250-9d16-090a987c0dbf.xml
- print.iolecvt\_encodeunicodename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 326a9374-7ed5-4521-999a-2c4c59faa617
keywords:
- EncodeUnicodeName 方法打印设备
- EncodeUnicodeName 方法打印设备，IOleCvt 接口
- IOleCvt 接口打印设备，EncodeUnicodeName 方法
topic_type:
- apiref
api_name:
- IOleCvt.EncodeUnicodeName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cca05c967042ef8a32b7c837badd59f4db6bebb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520332"
---
# <a name="iolecvtencodeunicodename-method"></a>IOleCvt::EncodeUnicodeName 方法

**EncodeUnicodeName**属性启用 ASP Web 页后，可以转换为其 Unicode 等效的 ANSI 字符串。

<a name="syntax"></a>语法
------

```cpp
[propget, id(2), helpstring("property EncodeUnicodeName")] HRESULT EncodeUnicodeName(
  [in]          BSTR bstrSrcName,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrSrcName* \[in\]  
调用方提供 ANSI 字符串转换。

*pVal* \[out, retval\]  
调用方提供位置将接收已转换的字符串的指针。

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
strMyUrl = "MyPage.asp?MyVariable=" & 
            OleCvt.EncodeUnicodeName("My&Unicode&Parameter")
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
