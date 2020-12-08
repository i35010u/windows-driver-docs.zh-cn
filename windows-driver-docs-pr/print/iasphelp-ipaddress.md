---
title: Iasphelp 获取 \_ IPAddress 方法
description: IPAddress 属性允许 ASP 网页获取打印机的 IP 地址。
MS-HAID:
- webfnc\_f0b5a4c6-50db-48a0-a10d-2a835cac32ac.xml
- print.iasphelp\_ipaddress
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 4676f3d09339c3aac4186ae19fa4b766c702108a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835783"
---
# <a name="iasphelpget_ipaddress-method"></a>Iasphelp：： get \_ IPAddress 方法

**IPAddress** 属性允许 ASP 网页获取打印机的 IP 地址。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IPAddress(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向接收指向 IP 地址字符串的指针的位置的指针。

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
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

在查询 **Iasphelp：： IPAddress** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

如果 TCP/IP 端口监视器不支持打印机，则返回的字符串为空。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)
