---
title: OID_GEN_TRANSMIT_BUFFER_SPACE
description: 为查询，OID_GEN_TRANSMIT_BUFFER_SPACE OID 以字节为单位指定的内存量，在适用于缓冲的 NIC 上传输数据。
ms.assetid: 23d242fc-8447-4660-ab84-b8cbdb638a71
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSMIT_BUFFER_SPACE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3fe56b00adf67686e5c510961039d3245dc54efc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387872"
---
# <a name="oidgentransmitbufferspace"></a>OID\_GEN\_传输\_缓冲区\_空间


为查询，OID\_GEN\_传输\_缓冲区\_空间 OID 以字节为单位指定的内存量，在适用于缓冲的 NIC 上传输数据。

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

一种协议可用于此 OID 作为指南大小调整的量将针对每个发送的数据传输。

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

 

 




