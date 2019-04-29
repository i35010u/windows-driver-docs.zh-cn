---
title: OID_GEN_PROTOCOL_OPTIONS
description: 作为一组 OID_GEN_PROTOCOL_OPTIONS OID 指定定义的协议驱动程序的可选属性的位掩码。
ms.assetid: 48c3468b-2d8b-48cb-9a25-19470923f582
ms.date: 08/08/2017
keywords: -OID_GEN_PROTOCOL_OPTIONS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c4fbfd8d7bf456986065325881f9740c4c3c1b7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367715"
---
# <a name="oidgenprotocoloptions"></a>OID\_GEN\_协议\_选项


作为一组 OID\_GEN\_协议\_选项 OID 指定定义的协议驱动程序的可选属性的位掩码。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 此 OID 是协议驱动程序。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

一种协议将通知 NDIS 其属性，可以根据需要充分利用它们。 如果协议驱动程序没有在绑定上设置它的标志，NDIS 认为它们是所有明文。

当前定义的以下标志：

<a href="" id="ndis-prot-option-estimated-length"></a>NDIS\_端口是否\_选项\_估计\_长度  
指定，可以指定数据包大小，而不是确切的值，此协议的最坏的情况估算值的数据包。

<a href="" id="ndis-prot-option-no-loopback"></a>NDIS\_端口是否\_选项\_否\_环回  
指定协议不需要在绑定上的环回支持。

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

 

 




