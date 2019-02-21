---
title: Iasphelp get\_SNMPSupported 方法
description: SNMPSupported 属性，以确定是否正在与打印机使用 SNMP 的 ASP Web 页。
MS-HAID:
- webfnc\_2128dc9d-a113-4061-a6c9-3ebe2a304dd5.xml
- print.iasphelp\_snmpsupported
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 17e3986b-3eb6-4c9d-ae4f-338e9cce439a
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
ms.openlocfilehash: e8991703d7aed966333bf2dd15d64901cd1f7b42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543513"
---
# <a name="iasphelpgetsnmpsupported-method"></a>Iasphelp::get\_SNMPSupported 方法

**SNMPSupported**属性，以确定是否正在与打印机使用 SNMP 的 ASP Web 页。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_SNMPSupported(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
调用方提供指向用于接收的位置 **，则返回 TRUE**如果正在使用 SNMP 打印机，或**FALSE**如果不是。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::SNMPSupported**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp::Open**](iasphelp-open.md)
