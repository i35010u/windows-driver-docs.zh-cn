---
title: Iasphelp get\_双工方法
description: 双工属性启用 ASP 网页，以确定是否打印机支持双面打印。
MS-HAID:
- webfnc\_346f6357-9ca9-4b97-93a3-50ec9f28c118.xml
- print.iasphelp\_duplex
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e837f8f2-68a5-4f9a-a253-dfcf33ea7047
keywords:
- get_Duplex 方法打印设备
- get_Duplex 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_Duplex 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_Duplex
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb48ac5aa4134c8b24cda828434a17c5c19e5f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542982"
---
# <a name="iasphelpgetduplex-method"></a>Iasphelp::get\_双工方法

**双工**属性启用 ASP 网页，以确定是否打印机支持双面打印。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Duplex(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
调用方提供指向用于接收的位置 **，则返回 TRUE**若打印机支持双面打印，或**FALSE**如果不是。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::Duplex**属性可以进行查询。

```vb
Dim objPrinter, DoesDuplex
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
DoesDuplex = objPrinter.Duplex
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

[**Iasphelp::Open**](iasphelp-open.md)
