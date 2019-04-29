---
title: Iasphelp get\_IsHTTP 方法
description: IsHTTP 属性启用 ASP 网页，以确定是否将打印机连接到 HTTP 端口。
MS-HAID:
- webfnc\_e3e58eea-498f-4e85-8072-2c49ac50d733.xml
- print.iasphelp\_ishttp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 54aaed11-8f18-433b-b774-c695a85b813e
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
ms.openlocfilehash: 9f6058d7e5de23aa7b556a7a87241dabfdaaa976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392851"
---
# <a name="iasphelpgetishttp-method"></a>Iasphelp::get\_IsHTTP 方法

**IsHTTP**属性启用 ASP 网页，以确定是否将打印机连接到 HTTP 端口。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IsHTTP(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
指向接收的内存位置的调用方提供指针 **，则返回 TRUE**如果打印机已连接到 HTTP 端口，并**FALSE**否则为。

<a name="return-value"></a>返回值
------------

下表中，该属性返回的值之一。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::IsHTTP**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::Open**](iasphelp-open.md)
