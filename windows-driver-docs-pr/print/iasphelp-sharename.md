---
title: Iasphelp get\_ShareName 方法
description: 共享名属性启用 ASP 网页，若要获取打印机的共享的名称。
MS-HAID:
- webfnc\_68b8e99e-a40b-44ee-94c8-2a8bcc293fa3.xml
- print.iasphelp\_sharename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: fdb93613-9c7f-49ea-b90e-684b63e6417a
keywords:
- get_ShareName 方法打印设备
- get_ShareName 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_ShareName 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_ShareName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805acbb28a55420e46e5a9fabef87475fa375fa8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541221"
---
# <a name="iasphelpgetsharename-method"></a>Iasphelp::get\_ShareName 方法

**ShareName**属性启用 ASP 网页，若要获取打印机的共享的名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_ShareName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
调用方提供指向用于接收指向共享名称字符串的指针的位置。

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
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>尚未调用方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::ShareName**属性可以进行查询。

```vb
Dim objPrinter, DrvrName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
DrvrName = objPrinter.ShareName
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

## <a name="see-also"></a>另请参阅

[**Iasphelp::Open**](iasphelp-open.md)
