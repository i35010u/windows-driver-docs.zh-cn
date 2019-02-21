---
title: Iasphelp 打开方法
description: Open 方法启用 ASP 网页，以打开到打印机的访问权限。
MS-HAID:
- webfnc\_7fa3a36d-4bf6-46d2-9336-e024d3aa1eec.xml
- print.iasphelp\_open
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: f4e39b76-3118-41d8-a5f8-501d884cbcdb
keywords:
- Open 方法打印设备
- Open 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，Open 方法
topic_type:
- apiref
api_name:
- Iasphelp.Open
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 499de74e720d5bd8c23880e7a64819e0df90420d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554697"
---
# <a name="iasphelpopen-method"></a>Iasphelp::Open 方法

**打开**方法启用 ASP 网页，以打开到打印机的访问权限。

<a name="syntax"></a>语法
------

```cpp
HRESULT Open(
  [in] BSTR bstrPrinterName
);
```

<a name="parameters"></a>参数
----------

*bstrPrinterName* \[in\]  
调用方提供包含打印机名称的字符串指针。

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
<td><strong>ERROR_INVALID_PRINTER_NAME</strong></td>
<td><p>无效的打印机名称。</p></td>
</tr>
<tr class="odd">
<td><strong>ERROR_NOT_ENOUGH_MEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法获取通过调用打印后台处理程序的访问指定打印机**OpenPrinter**函数。 有关此函数的详细信息，请参阅 Windows SDK 文档。

之后**Iasphelp::Open**调用时，打印机保持打开状态，直到[ **Iasphelp::Close** ](iasphelp-close.md)调用方法时，或直到**Iasphelp::Open**具有不同的打印机名称再次调用。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp::Close**](iasphelp-close.md)
