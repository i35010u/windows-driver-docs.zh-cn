---
title: Iasphelp get\_SNMPDevice 方法
description: SNMPDevice 属性启用 ASP 网页，以获取打印机的 SNMP 设备索引 （根据 RFC 1759 的定义）。
MS-HAID:
- webfnc\_e4a9d1b3-1168-45a7-98cb-9c19fdf83009.xml
- print.iasphelp\_snmpdevice
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 4ae42406-6a19-4af0-88c5-bc4375bb648c
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
ms.openlocfilehash: ae5eec7ac38d7a5dc782f2bc36c8d0019015c7c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365490"
---
# <a name="iasphelpgetsnmpdevice-method"></a>Iasphelp::get\_SNMPDevice 方法

**SNMPDevice**属性启用 ASP 网页，以获取打印机的 SNMP 设备索引 （根据 RFC 1759 的定义）。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_SNMPDevice(
  [out] DWORD *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
要接收一个数值表示打印机的 SNMP 设备索引的调用方提供的位置。

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

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::SNMPDevice**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp::Open**](iasphelp-open.md)
