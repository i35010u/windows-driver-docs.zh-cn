---
title: Iasphelp get \_ 双工方法
description: 使用双工属性可以使 ASP 网页确定打印机是否支持双面打印。
MS-HAID:
- webfnc\_346f6357-9ca9-4b97-93a3-50ec9f28c118.xml
- print.iasphelp\_duplex
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: e9c55c76687374d36071cfb8d87312b4b79f8de5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835791"
---
# <a name="iasphelpget_duplex-method"></a>Iasphelp：： get \_ 双工方法

使用 **双工** 属性可以使 ASP 网页确定打印机是否支持双面打印。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Duplex(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
如果打印机支持双面打印，则调用方提供的指向位置的指针为 **TRUE** ; 否则为 **FALSE** 。

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

在查询 **Iasphelp：:D uplex** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)
