---
title: Iasphelp get \_ SNMPSupported 方法
description: 使用 SNMPSupported 属性可以使 ASP 网页确定是否正在将 SNMP 与打印机一起使用。
MS-HAID:
- webfnc\_2128dc9d-a113-4061-a6c9-3ebe2a304dd5.xml
- print.iasphelp\_snmpsupported
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_SNMPSupported 方法打印设备
- get_SNMPSupported 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_SNMPSupported 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_SNMPSupported
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba3f5ce1db5958fed82ecd8b5d376efa6bbfc462
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796777"
---
# <a name="iasphelpget_snmpsupported-method"></a>Iasphelp：： get \_ SNMPSupported 方法

使用 **SNMPSupported** 属性可以使 ASP 网页确定是否正在将 SNMP 与打印机一起使用。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_SNMPSupported(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向接收的位置的指针，如果正在将 SNMP 与打印机一起使用，则为 **TRUE** ; 否则为 **FALSE** 。

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

在查询 **Iasphelp：： SNMPSupported** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, UsingSNMP
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
UsingSNMP = objPrinter.SNMPSupported
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
