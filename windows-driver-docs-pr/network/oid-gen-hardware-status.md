---
title: OID_GEN_HARDWARE_STATUS
description: 作为查询，OID_GEN_HARDWARE_STATUS OID 指定基础 NIC 的当前硬件状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_HARDWARE_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2d61bcba1fd89905bccb8d7ce8b57f12312ccda6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832147"
---
# <a name="oid_gen_hardware_status"></a>OID \_ 生成 \_ 硬件 \_ 状态


作为查询，OID \_ 代 \_ 硬件 \_ 状态 OID 指定基础 NIC 的当前硬件状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
已过时。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

OID 生成 \_ \_ 硬件 \_ 状态 OID 将基础 NIC 的当前硬件状态指定为下列 NDIS \_ 硬件 \_ 状态类型值之一：

<a href="" id="ndishardwarestatusready"></a>**NdisHardwareStatusReady**  
可用且能够通过网络发送和接收数据

<a href="" id="ndishardwarestatusinitializing"></a>**NdisHardwareStatusInitializing**  
正在初始化

<a href="" id="ndishardwarestatusreset"></a>**NdisHardwareStatusReset**  
重置

<a href="" id="ndishardwarestatusclosing"></a>**NdisHardwareStatusClosing**  
关闭

<a href="" id="ndishardwarestatusnotready"></a>**NdisHardwareStatusNotReady**  
未准备就绪

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

 

 




