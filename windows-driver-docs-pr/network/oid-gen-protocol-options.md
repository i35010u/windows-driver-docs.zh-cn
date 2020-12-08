---
title: OID_GEN_PROTOCOL_OPTIONS
description: 作为集，OID_GEN_PROTOCOL_OPTIONS OID 指定了一个位掩码，该位掩码定义了协议驱动程序的可选属性。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PROTOCOL_OPTIONS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b0096dc12d72355c07e1a15902614dccb8a75d78
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829429"
---
# <a name="oid_gen_protocol_options"></a>OID \_ 生成 \_ 协议 \_ 选项


作为集，OID 生成 \_ \_ 协议 \_ 选项 oid 指定定义协议驱动程序的可选属性的位掩码。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 此 OID 适用于协议驱动程序。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

协议会将其属性告知 NDIS，可以选择利用它们。 如果协议驱动程序没有在绑定上设置其标志，NDIS 会假设它们全都清楚。

当前定义了下列标志：

<a href="" id="ndis-prot-option-estimated-length"></a>NDIS \_ PROT \_ 选项 \_ 估计 \_ 长度  
指定在对此协议的数据包大小的最差情况下（而不是精确值），可以指示数据包。

<a href="" id="ndis-prot-option-no-loopback"></a>NDIS \_ PROT \_ 选项 \_ 无 \_ 环回  
指定协议不需要对绑定的环回支持。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

 

 




