---
title: Iasphelp get \_ ErrorDscp 方法
description: 使用 ErrorDscp 属性，ASP 网页可以将错误代码转换为描述性字符串。
MS-HAID:
- webfnc\_55f547fe-4cbe-4905-b268-afd7af400de4.xml
- print.iasphelp\_errordscp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: c05c9957cd11112317223c57edc0269cd3151c7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796821"
---
# <a name="iasphelpget_errordscp-method"></a>Iasphelp：： get \_ ErrorDscp 方法

使用 **ErrorDscp** 属性，ASP 网页可以将错误代码转换为描述性字符串。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_ErrorDscp(
  [in]  long lErrCode,
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*lErrCode* \[中\]  
指定要转换为描述性字符串的错误代码。

*pVal* \[弄\]  
调用方提供的指针，该指针指向接收与 *lErrCode* 参数中的错误代码相对应的描述性字符串的位置。

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
<td><p>未调用 <strong>Iasphelp：： Open</strong> 方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_POINTER</strong></td>
<td><p><em>PVal</em>指针无效。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

在查询 **Iasphelp：： ErrorDscp** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)
