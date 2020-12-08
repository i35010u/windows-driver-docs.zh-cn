---
title: Iasphelp 获取 \_ 共享名方法
description: "\"共享名\" 属性允许 ASP 网页获取打印机的共享名称。"
MS-HAID:
- webfnc\_68b8e99e-a40b-44ee-94c8-2a8bcc293fa3.xml
- print.iasphelp\_sharename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 5f640d75fb7f0a6fedd632f258e9b96d08f42f0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796781"
---
# <a name="iasphelpget_sharename-method"></a>Iasphelp：：获取 \_ 共享名方法

" **共享** 名" 属性允许 ASP 网页获取打印机的共享名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_ShareName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向接收指向共享名称字符串的指针的位置的指针。

<a name="return-value"></a>返回值
------------

也可以返回 Win32 错误代码。

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
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

必须先调用 [**Iasphelp：： Open**](iasphelp-open.md) 方法，然后才能查询 **Iasphelp：：共享名** 属性。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)
