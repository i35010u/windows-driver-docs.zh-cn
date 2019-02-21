---
title: OID_GEN_TRANSMIT_BLOCK_SIZE
description: 为查询，OID_GEN_TRANSMIT_BLOCK_SIZE OID 指定最小的单个网络数据包占用的字节数中的 NIC 的传输缓冲区空间
ms.assetid: 81874999-029a-4e7e-8dbe-fc8e34bcae67
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_TRANSMIT_BLOCK_SIZE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 128b017418cbc9d1dc7f7d2c6464845acab3f235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555407"
---
# <a name="oidgentransmitblocksize"></a>OID\_GEN\_传输\_阻止\_大小


为查询，OID\_GEN\_传输\_阻止\_大小 OID NIC 的传输缓冲区空间中指定的最小单个 net 数据包占用的字节数

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

OID\_GEN\_传输\_阻止\_大小 OID NIC 的传输缓冲区空间中指定的最小单个 net 数据包占用的字节数 例如，具有传输空间分割成 256 字节块 NIC 必须的传输块大小为 256 个字节。 若要计算此类 NIC 上的总传输缓冲空间，其驱动程序乘以的 NIC 上的传输缓冲区的数目及其传输块大小。

对于其他的 Nic，传输块大小等同于其最大数据包大小。

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

 

 




