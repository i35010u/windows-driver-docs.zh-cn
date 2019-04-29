---
title: Iasphelp get\_ErrorDscp 方法
description: ErrorDscp 属性启用 ASP Web 页后，可以将错误代码转换为的描述性字符串。
MS-HAID:
- webfnc\_55f547fe-4cbe-4905-b268-afd7af400de4.xml
- print.iasphelp\_errordscp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 46d44c54-4fd5-489f-9624-1df3c8917237
keywords:
- get_ErrorDscp 方法打印设备
- get_ErrorDscp 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_ErrorDscp 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_ErrorDscp
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16568f8224786cabf4b8a857d0d87de3bfe62173
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392888"
---
# <a name="iasphelpgeterrordscp-method"></a>Iasphelp::get\_ErrorDscp 方法

**ErrorDscp**属性启用 ASP Web 页后，可以将错误代码转换为的描述性字符串。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_ErrorDscp(
  [in]  long lErrCode,
  [out] BSTR *pVal
);
```

<a name="parameters"></a>Parameters
----------

*lErrCode* \[in\]  
指定要转换为描述性字符串的错误代码。

*pVal* \[out\]  
指向接收对应于中的错误代码的描述性字符串的位置的调用方提供指针*lErrCode*参数。

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
<td><p><strong>Iasphelp::Open</strong>尚未调用方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_POINTER</strong></td>
<td><p>无效<em>pVal</em>指针。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::ErrorDscp**属性可以进行查询。

```vb
Dim objPrinter, ErrorCode, ErrorString
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
...
' Get error code.
...
ErrorString = objPrinter.ErrorDscp(ErrorCode)
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
