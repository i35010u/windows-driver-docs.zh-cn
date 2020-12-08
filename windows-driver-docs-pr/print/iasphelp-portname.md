---
title: Iasphelp get \_ portvalue 方法
description: 使用 Portvalue 属性可以使 ASP 网页获取打印机的端口名称。
MS-HAID:
- webfnc\_67f21c2f-9caf-4cd0-8a4b-df4ab9f63b43.xml
- print.iasphelp\_portname
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_PortName 方法打印设备
- get_PortName 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_PortName 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_PortName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70b451e50adbb58c8790d7daa08bf2f30f57aeec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796783"
---
# <a name="iasphelpget_portname-method"></a>Iasphelp：： get \_ portvalue 方法

使用 **portvalue** 属性可以使 ASP 网页获取打印机的端口名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PortName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的位置，用于接收指向表示打印机端口名称的字符串的指针。

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

在查询 **Iasphelp：:P ortname** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, PtrPortName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrPortName = objPrinter.PortName
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
