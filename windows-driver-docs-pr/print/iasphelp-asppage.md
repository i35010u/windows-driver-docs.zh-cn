---
title: Iasphelp get\_AspPage 方法
description: AspPage 属性启用 ASP 网页，以获取用于描述特定于打印机的详细信息的初始 ASP 文件的目录路径。
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
ms.openlocfilehash: f40d9320c8ac462432598094e3e77979ca5afced
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360474"
---
# <a name="iasphelpgetasppage-method"></a>Iasphelp::get\_AspPage 方法


**AspPage**属性启用 ASP 网页，以获取用于描述特定于打印机的详细信息的初始 ASP 文件的目录路径。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_AspPage(
  [in]  DWORD dwPage,
  [out] BSTR  *pVal
);
```

<a name="parameters"></a>Parameters
----------

*dwPage* \[in\]  
必须为 1。

*pVal* \[out\]  
调用方提供的位置以接收指定初始 Web 页面描述特定于打印机的详细信息的目录路径的大小前缀的 Unicode 字符串指针。

<a name="return-value"></a>返回值
------------

此方法可以返回下列值之一。

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
<td><strong>E_NOTIMPL</strong></td>
<td><p>ASP 文件不可用。</p></td>
</tr>
<tr class="even">
<td><strong>E_POINTER</strong></td>
<td><p>无效<em>pVal</em>指针。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

若要确定在哪里可以找到页面的 ASP 文件，该方法使用的算法中所述[将显示该打印机的详细信息页？](https://docs.microsoft.com/windows-hardware/drivers/print/which-printer-details-page-is-displayed-)。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::AspPage**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::Open**](iasphelp-open.md)
