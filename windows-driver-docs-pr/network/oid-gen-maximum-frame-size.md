---
title: OID_GEN_MAXIMUM_FRAME_SIZE
description: 为查询，OID_GEN_MAXIMUM_FRAME_SIZE OID 指定最大网络数据包大小，以字节为单位，NIC 支持。
ms.assetid: 4c81f3a6-6f66-466d-8d22-67841a5a8320
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_FRAME_SIZE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8079f279baa2e230301db058eb0f6671c97270e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520589"
---
# <a name="oidgenmaximumframesize"></a>OID\_GEN\_MAXIMUM\_FRAME\_SIZE


为查询，OID\_GEN\_最大\_帧\_大小 OID 指定最大网络数据包大小，以字节为单位，NIC 支持。 此规范不包括标头。

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

在初始化过程并在重新启动，微型端口驱动程序提供的最大帧大小。 NDIS NDIS 6.0 和更高版本的微型端口驱动程序处理此 OID 查询。

请求传输到此查询响应，微型端口驱动程序应指示可以发送传输，不包括标头的最大帧大小。 模拟另一种中等类型绑定到传输的微型端口驱动程序必须确保协议提供网络数据包的最大帧大小不超过真实网络中的大小限制。 同样适用于支持要求在帧中插入字段的 NIC 的微型端口驱动程序。 例如，若要确定最大传输单元 (MTU)，传输发送此查询到 nic。

如果微型端口驱动程序所支持的 802.1p 数据包优先级和 802.1Q 虚拟 LAN (VLAN) 标记，如果微型端口驱动程序需要优先级值将被删除之前，框架必须经过旧网络基于先前的操作，可能表示该微型端口驱动程序对此查询响应中的较小值。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




