---
title: Iasphelp get \_ IsHTTP 方法
description: 使用 IsHTTP 属性可以使 ASP 网页确定打印机是否已连接到 HTTP 端口。
MS-HAID:
- webfnc\_e3e58eea-498f-4e85-8072-2c49ac50d733.xml
- print.iasphelp\_ishttp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_IsHTTP 方法打印设备
- get_IsHTTP 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_IsHTTP 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_IsHTTP
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 372ed2860d95cd5a7553ffc388ed31a2726ce08d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835779"
---
# <a name="iasphelpget_ishttp-method"></a>Iasphelp：： get \_ IsHTTP 方法

使用 **IsHTTP** 属性可以使 ASP 网页确定打印机是否已连接到 HTTP 端口。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IsHTTP(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
如果打印机连接到 HTTP 端口，则调用方提供的指向内存位置的指针，如果打印机已连接到 HTTP 端口，则为 **TRUE** ; 否则为 **FALSE** 。

<a name="return-value"></a>返回值
------------

属性返回下表中的值之一。

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

在查询 **Iasphelp：： IsHTTP** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, IsHTTPPort
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
IsHTTPPort = objPrinter.IsHTTP
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
