---
title: Iasphelp Open 方法
description: Open 方法使 ASP 网页能够打开对打印机的访问。
MS-HAID:
- webfnc\_7fa3a36d-4bf6-46d2-9336-e024d3aa1eec.xml
- print.iasphelp\_open
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 打开方法打印设备
- 开放式方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，Open 方法
topic_type:
- apiref
api_name:
- Iasphelp.Open
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3842a918468e2b731ad25495964d4610b966a7a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835763"
---
# <a name="iasphelpopen-method"></a>Iasphelp：： Open 方法

**Open** 方法使 ASP 网页能够打开对打印机的访问。

<a name="syntax"></a>语法
------

```cpp
HRESULT Open(
  [in] BSTR bstrPrinterName
);
```

<a name="parameters"></a>参数
----------

*bstrPrinterName* \[中\]  
调用方提供的指向包含打印机名称的字符串的指针。

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
<td><strong>ERROR_INVALID_PRINTER_NAME</strong></td>
<td><p>打印机名称无效。</p></td>
</tr>
<tr class="odd">
<td><strong>ERROR_NOT_ENOUGH_MEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法通过调用打印后台处理程序的 **OpenPrinter** 函数获取对指定打印机的访问。 有关此函数的详细信息，请参阅 Windows SDK 文档。

在 **Iasphelp：： Open** 调用之后，打印机将一直保持打开状态，直到调用 [**Iasphelp：： Close**](iasphelp-close.md) 方法，或直到再次使用不同的打印机名称调用 **Iasphelp：： Open** 。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
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

[**Iasphelp：： Close**](iasphelp-close.md)
