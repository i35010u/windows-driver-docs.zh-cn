---
title: Iasphelp get\_IsTCPMonSupported 方法
description: IsTCPMonSupported 属性启用 ASP 网页，以确定如果打印机正在使用 Microsoft 的标准 TCP/IP 端口监视器。
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
ms.openlocfilehash: e7d4a3958e062ce9501dd2d12b805cad6e6ad18a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567788"
---
# <a name="iasphelpgetistcpmonsupported-method"></a>Iasphelp::get\_IsTCPMonSupported 方法

**IsTCPMonSupported**属性启用 ASP 网页，以确定 Microsoft 的标准 TCP/IP[端口监视器](https://docs.microsoft.com/windows-hardware/drivers/print/port-monitors)与打印机一起使用。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IsTCPMonSupported(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供指向用于接收的位置 **，则返回 TRUE**如果打印机正在使用的 TCP/IP 端口监视器或**FALSE**如果不是。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::IsTCPMonSupported**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::Open**](iasphelp-open.md)
