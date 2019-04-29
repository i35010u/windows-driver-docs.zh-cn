---
title: Iasphelp get\_IPAddress 方法
description: IPAddress 属性启用 ASP 网页获取打印机的 IP 地址。
MS-HAID:
- webfnc\_f0b5a4c6-50db-48a0-a10d-2a835cac32ac.xml
- print.iasphelp\_ipaddress
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 535ea9fa-fff7-47fd-84ae-f61526f1b622
keywords:
- get_IPAddress 方法打印设备
- get_IPAddress 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_IPAddress 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_IPAddress
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bf6125f58ca21bddae590c8a738daca1d50ff10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392879"
---
# <a name="iasphelpgetipaddress-method"></a>Iasphelp::get\_IPAddress 方法

**IPAddress**属性启用 ASP 网页获取打印机的 IP 地址。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IPAddress(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供指向用于接收指向 IP 地址字符串的指针的位置。

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
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::IPAddress**属性可以进行查询。

如果打印机不支持通过 TCP/IP 端口监视器，则返回的字符串为空。

```vb
Dim objPrinter, PrinterIP
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PrinterIP = objPrinter.IPAddress
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
