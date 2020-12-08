---
title: Iasphelp get \_ SNMPDevice 方法
description: SNMPDevice 属性使 ASP 网页能够按 RFC 1759) 的定义 (获取打印机的 SNMP 设备索引。
MS-HAID:
- webfnc\_e4a9d1b3-1168-45a7-98cb-9c19fdf83009.xml
- print.iasphelp\_snmpdevice
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_SNMPDevice 方法打印设备
- get_SNMPDevice 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_SNMPDevice 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_SNMPDevice
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191eb49a766831f9dab2686315cdf41ab2612777
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835733"
---
# <a name="iasphelpget_snmpdevice-method"></a>Iasphelp：： get \_ SNMPDevice 方法

**SNMPDevice** 属性使 ASP 网页能够按 RFC 1759) 的定义 (获取打印机的 SNMP 设备索引。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_SNMPDevice(
  [out] DWORD *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的位置，用于接收表示打印机 SNMP 设备索引的数字值。

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

在查询 **Iasphelp：： SNMPDevice** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, SNMPDeviceIndex
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
SNMPDeviceIndex = objPrinter.SNMPDevice
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
