---
title: ISNMP Open 方法
description: 使用 Open 方法，ASP 网页可以创建到指定 SNMP 代理的通信路径。
MS-HAID:
- webfnc\_2be497fa-98d8-4fb3-997c-fa1345ed4648.xml
- print.isnmp\_open
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 打开方法打印设备
- 开放式方法打印设备，ISNMP 接口
- ISNMP 接口打印设备，Open 方法
topic_type:
- apiref
api_name:
- ISNMP.Open
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc99c544b0ac4de0521796c27430092348343758
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835503"
---
# <a name="isnmpopen-method"></a>ISNMP：： Open 方法

`Open`方法使 ASP 网页能够创建到指定 SNMP 代理的通信路径。

<a name="syntax"></a>语法
------

```cpp
HRESULT Open(
  [in] BSTR    bstrHost,
  [in] BSTR    bstrCommunity,
  [in] VARIANT varRetry,
  [in] VARIANT varTimeout
);
```

<a name="parameters"></a>参数
----------

*bstrHost* \[中\]  
调用方提供的指向标识 SNMP 代理系统的字符串的指针。 此 IP 地址可以是以点分隔的 IP 地址，也可以是可解析为 IP 地址的主机名、IPX 地址 (8.12 表示法) 或以太网地址。

*bstrCommunity* \[中\]  
调用方提供的指向字符串的指针，该字符串表示 SNMP 代理系统的社区名称。

*varRetry* \[中\]  
可选，调用方提供的重试值。 如果未指定，则使用默认值。 建议值为2。

*varTimeout* \[中\]  
可选，调用方提供的超时值（以毫秒为单位）。 如果未指定，则使用默认值。 建议值为1000。

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
<td><strong>E_INVALIDARG</strong></td>
<td><p>无法将 <em>varRetry</em> 或 <em>varTimeOut</em> 值转换为短整型。</p></td>
</tr>
<tr class="odd">
<td><strong>E_FAIL</strong></td>
<td><p>对 <strong>SnmpMgrOpen</strong> 的调用失败。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法调用 **SnmpMgrOpen** 函数，该函数与具有相同的参数 `ISNMP::Open` 。 有关此函数的详细信息，请参阅 Windows SDK 文档。

调用后 `ISNMP::Open` ，SNMP 代理的通信路径保持打开状态，直到调用 [**ISNMP：： Close**](isnmp-close.md) 方法或 `ISNMP::Open` 再次调用。

```vb
Dim StrIP, strCommunity, objSNMP
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
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
<tr class="odd">
<td><p>标头</p></td>
<td>Olesnmp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**ISNMP：： Close**](isnmp-close.md)
