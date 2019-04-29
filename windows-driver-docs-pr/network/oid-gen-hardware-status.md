---
title: OID_GEN_HARDWARE_STATUS
description: 为查询，OID_GEN_HARDWARE_STATUS OID 指定新的硬件状态的基础的 nic。
ms.assetid: beab6f7a-b064-446f-8008-ef8db9d7c080
ms.date: 08/08/2017
keywords: -OID_GEN_HARDWARE_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: de190f8dd238d047a9ccc9653321edd9b439df5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381347"
---
# <a name="oidgenhardwarestatus"></a>OID\_GEN\_硬件\_状态


为查询，OID\_GEN\_硬件\_状态 OID 指定新的硬件状态的基础的 nic。

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

OID\_GEN\_硬件\_状态 OID 作为以下 NDIS 之一指定基础 NIC 的新的硬件状态\_硬件\_状态类型的值：

<a href="" id="ndishardwarestatusready"></a>**NdisHardwareStatusReady**  
可用并能够发送和接收数据而无法通过网络

<a href="" id="ndishardwarestatusinitializing"></a>**NdisHardwareStatusInitializing**  
初始化

<a href="" id="ndishardwarestatusreset"></a>**NdisHardwareStatusReset**  
重置

<a href="" id="ndishardwarestatusclosing"></a>**NdisHardwareStatusClosing**  
关闭

<a href="" id="ndishardwarestatusnotready"></a>**NdisHardwareStatusNotReady**  
未就绪

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




