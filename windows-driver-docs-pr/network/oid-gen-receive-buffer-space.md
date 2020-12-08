---
title: OID_GEN_RECEIVE_BUFFER_SPACE
description: 作为查询，OID_GEN_RECEIVE_BUFFER_SPACE OID 指定可用于缓冲接收数据的 NIC 上的内存量。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_BUFFER_SPACE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b822b1d2e52af3223c2cf71899871787cdf3b1c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818841"
---
# <a name="oid_gen_receive_buffer_space"></a>OID \_ 生成 \_ 接收 \_ 缓冲区 \_ 空间


作为查询，OID 生成 \_ \_ 接收 \_ 缓冲区 \_ 空间 oid 指定可用于缓冲接收数据的 NIC 上的内存量。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

在使用远程节点建立会话之后，协议驱动程序可以使用此 OID 作为接收窗口的播发。

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

 

 




