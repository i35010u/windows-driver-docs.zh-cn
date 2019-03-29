---
title: Iasphelp get\_DriverName 方法
description: DriverName 属性启用 ASP 网页，若要获取的打印机驱动程序名称。
MS-HAID:
- webfnc\_99826bd3-a4fb-41b4-9f05-10598c4fcc01.xml
- print.iasphelp\_drivername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 656c8d36-23c0-46ae-81fd-a1123d5ab068
keywords:
- get_DriverName 方法打印设备
- get_DriverName 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_DriverName 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_DriverName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28776d64f6c6e405c5535d6e6f662571c8f8bccb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565603"
---
# <a name="iasphelpgetdrivername-method"></a>Iasphelp::get\_DriverName 方法

**DriverName**属性启用 ASP 网页，若要获取的打印机驱动程序名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_DriverName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供指向用于接收指向驱动程序名称字符串的指针的位置。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::DriverName**属性可以进行查询。

```vb
Dim objPrinter, DrvrName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
DrvrName = objPrinter.DriverName
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
