---
title: Iasphelp get\_PortName 方法
description: PortName 属性启用 ASP 网页，以获取打印机的端口名称。
MS-HAID:
- webfnc\_67f21c2f-9caf-4cd0-8a4b-df4ab9f63b43.xml
- print.iasphelp\_portname
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 2696d5c4-e1a1-4d9f-b5f5-e2083b548c65
keywords:
- get_PortName 方法打印设备
- get_PortName 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_PortName 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_PortName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78fc8e502c925e16cc3958f2e7ee70f90a658989
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358739"
---
# <a name="iasphelpgetportname-method"></a>Iasphelp::get\_PortName 方法

**PortName**属性启用 ASP 网页，以获取打印机的端口名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PortName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
要接收指向表示打印机的端口名称的字符串的指针的调用方提供的位置。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::PortName**属性可以进行查询。

```vb
Dim objPrinter, PtrPortName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrPortName = objPrinter.PortName
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
