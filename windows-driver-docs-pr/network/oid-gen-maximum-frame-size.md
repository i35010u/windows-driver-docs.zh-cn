---
title: OID_GEN_MAXIMUM_FRAME_SIZE
description: 作为查询，OID_GEN_MAXIMUM_FRAME_SIZE OID 指定 NIC 支持的最大网络数据包大小（以字节为单位）。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_FRAME_SIZE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1fd535cdb8560f706ac145ccde1ad7714884d9e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821277"
---
# <a name="oid_gen_maximum_frame_size"></a>OID \_ GEN \_ 最大 \_ 帧 \_ 大小


作为查询，OID \_ GEN \_ 最大 \_ 帧 \_ 大小 oid 指定 NIC 支持的最大网络数据包大小（以字节为单位）。 此规范不包含标头。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

小型端口驱动程序在初始化期间和重启期间提供最大帧大小。 NDIS 为 NDIS 6.0 和更高的微型端口驱动程序处理此 OID 查询。

为了响应来自请求传输的此查询，微型端口驱动程序应指示传输可以发送的最大帧大小（不包括标头）。 模拟另一种介质类型以绑定到传输的微型端口驱动程序必须确保协议提供的网络数据包的最大帧大小不超过真实网络媒体的大小限制。 对于支持需要在帧中插入字段的 NIC 的微型端口驱动程序也是如此。 例如，若要确定最大传输单位 (MTU) ，传输将此查询发送到 NIC。

如果微型端口驱动程序支持 802.1 p 包优先级和 802.1 Q 虚拟 LAN (VLAN) 标记，这是基于之前的操作，如果微型端口驱动程序在删除优先级值之前要求帧必须遍历旧网络，则该微型端口驱动程序可能会指示响应此查询的较小值。

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

 

 




