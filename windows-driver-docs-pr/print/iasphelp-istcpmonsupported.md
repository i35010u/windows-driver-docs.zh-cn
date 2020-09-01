---
title: Iasphelp get \_ IsTCPMonSupported 方法
description: 使用 IsTCPMonSupported 属性可以确定是否将 Microsoft 的标准 TCP/IP 端口监视器与打印机一起使用。
MS-HAID:
- webfnc\_54f72229-524a-4bf2-917d-6a3ffcc27959.xml
- print.iasphelp\_istcpmonsupported
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 79ec0584-183d-476d-aca2-e85479248091
keywords:
- get_IsTCPMonSupported 方法打印设备
- get_IsTCPMonSupported 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_IsTCPMonSupported 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_IsTCPMonSupported
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d9f4524d25ca803f0cd21292ee2b7a7b3b5958a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209561"
---
# <a name="iasphelpget_istcpmonsupported-method"></a>Iasphelp：： get \_ IsTCPMonSupported 方法

使用 **IsTCPMonSupported** 属性可以确定是否将 Microsoft 的标准 tcp/ip [端口监视器](./port-monitors.md) 与打印机一起使用。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IsTCPMonSupported(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向要在打印机上使用 TCP/IP 端口监视器时接收 **TRUE** 的位置的指针; 如果不是，则为 **FALSE** 。

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

在查询**Iasphelp：： IsTCPMonSupported**属性之前，必须先调用[**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, UseStdMon
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
UseStdMon = objPrinter.IsTCPMonSupported
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
<td>“桌面”</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp：： Open**](iasphelp-open.md)