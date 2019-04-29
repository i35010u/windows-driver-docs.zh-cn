---
title: OID_GEN_RECEIVE_BUFFER_SPACE
description: 为查询，OID_GEN_RECEIVE_BUFFER_SPACE OID 为缓冲接收数据是可用的 NIC 上指定内存的量。
ms.assetid: 6eec18fa-22cd-4f65-acf4-0dd438dea2ff
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_BUFFER_SPACE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2ea0f96e6949e58a17333e6cf0f6e742d6533acb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391031"
---
# <a name="oidgenreceivebufferspace"></a>OID\_GEN\_RECEIVE\_BUFFER\_SPACE


为查询，OID\_GEN\_接收\_缓冲区\_空间 OID 为缓冲接收数据是可用的 NIC 上指定的内存量。

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

协议驱动程序可以使用此 OID 作为指南用于广告宣传其接收窗口后它在建立与远程节点的会话。

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

 

 




