---
title: ISNMP Open 方法
description: Open 方法启用 ASP Web 页后，可以创建指定的 SNMP 代理的通信路径。
MS-HAID:
- webfnc\_2be497fa-98d8-4fb3-997c-fa1345ed4648.xml
- print.isnmp\_open
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: a5d1a8a2-5953-4b7f-8f8e-cb84520ae9e8
keywords:
- Open 方法打印设备
- Open 方法打印设备，ISNMP 接口
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
ms.openlocfilehash: e5f5975b57e19f5dda2cb96ffe5788b1e9d14835
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533779"
---
# <a name="isnmpopen-method"></a>ISNMP::Open 方法

`Open`方法启用 ASP Web 页后，可以创建指定的 SNMP 代理的通信路径。

<a name="syntax"></a>语法
------

```cpp
HRESULT Open(
  [in] BSTR    bstrHost,
  [in] BSTR    bstrCommunity,
  [in] VARIANT varRetry,
  [in] VARIANT varTimeout
);
```

<a name="parameters"></a>参数
----------

*bstrHost* \[in\]  
调用方提供标识 SNMP 代理系统的字符串指针。 这可以是点分十进制 IP 地址或可被解析为 IP 地址、 IPX 地址 （采用 8.12 表示法） 或以太网地址的主机名称。

*bstrCommunity* \[in\]  
调用方提供表示 SNMP 代理系统的社区名称的字符串指针。

*varRetry* \[in\]  
可选的调用方提供的重试值。 如果未指定，使用默认值。 建议的值为 2。

*varTimeout* \[in\]  
可选的调用方提供的超时值，以毫秒为单位。 如果未指定，使用默认值。 建议的值为 1000年。

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
<td><strong>E_INVALIDARG</strong></td>
<td><p>任一<em>varRetry</em>或<em>varTimeOut</em>值无法转换为短整型。</p></td>
</tr>
<tr class="odd">
<td><strong>E_FAIL</strong></td>
<td><p>在调用<strong>SnmpMgrOpen</strong>失败。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法调用**SnmpMgrOpen**函数，它具有相同的参数作为`ISNMP::Open`。 有关此函数的详细信息，请参阅 Windows SDK 文档。

之后`ISNMP::Open`调用中，SNMP 代理的通信路径保持打开状态，直到[ **ISNMP::Close** ](isnmp-close.md)调用方法时，或直到`ISNMP::Open`再次调用。

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
<td>桌面设备</td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Olesnmp.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**ISNMP::Close**](isnmp-close.md)
