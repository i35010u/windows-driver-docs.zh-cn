---
title: Iasphelp get \_ AspPage 方法
description: 使用 AspPage 属性可以使 ASP 网页获取用于描述特定于打印机的详细信息的初始 ASP 文件的目录路径。
MS-HAID:
- webfnc\_6b636ee3-bc4f-4fbd-8ad9-87d6abcf3b35.xml
- print.iasphelp\_asppage
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 325c0666-b4c4-48b5-b14f-bdb81e1ee5d2
keywords:
- get_AspPage 方法打印设备
- get_AspPage 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_AspPage 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_AspPage
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96384e717c5ae648ce4680487cfd460f1b067ac0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210611"
---
# <a name="iasphelpget_asppage-method"></a>Iasphelp：： get \_ AspPage 方法


使用 **AspPage** 属性可以使 ASP 网页获取用于描述特定于打印机的详细信息的初始 ASP 文件的目录路径。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_AspPage(
  [in]  DWORD dwPage,
  [out] BSTR  *pVal
);
```

<a name="parameters"></a>参数
----------

*dwPage* \[中\]  
必须为 1。

*pVal* \[弄\]  
调用方提供的用于接收大小为前缀的 Unicode 字符串的位置的指针，该位置指定描述特定于打印机的详细信息的初始网页的目录路径。

<a name="return-value"></a>返回值
------------

此方法可以返回这些值之一。

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
<td><p>未调用 <a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"><strong>Iasphelp：： Open</strong></a> 方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_NOTIMPL</strong></td>
<td><p>ASP 文件不可用。</p></td>
</tr>
<tr class="even">
<td><strong>E_POINTER</strong></td>
<td><p><em>PVal</em>指针无效。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

若要确定在何处查找页面的 ASP 文件，该方法使用 [显示 "打印机详细信息" 页](./which-printer-details-page-is-displayed-.md)中所述的算法？。

在查询**Iasphelp：： AspPage**属性之前，必须先调用[**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
    Dim objPrinter, strPrinter, str
    strPrinter = Session("MS_printer")
    Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
    objPrinter.Open strPrinter
    str = objPrinter.ASPPage(1)
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
<td>“桌面”</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp：： Open**](iasphelp-open.md)