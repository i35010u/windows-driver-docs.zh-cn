---
title: OID_GEN_MAXIMUM_TOTAL_SIZE
description: 为查询，OID_GEN_MAXIMUM_TOTAL_SIZE OID 指定最大的数据包总长度，以字节为单位，NIC 支持。
ms.assetid: 4973b4bd-58a5-4242-b33f-1ff8c3a7ec4b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_TOTAL_SIZE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 27d2ba749322220f7efde2885ff452c09877ca99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540726"
---
# <a name="oidgenmaximumtotalsize"></a>OID\_GEN\_最大\_总\_大小


为查询，OID\_GEN\_最大\_总\_大小 OID 指定最大的数据包总长度，以字节为单位，NIC 支持。 此规范包含标头。

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

返回的长度指定基础媒体的最大数据包大小。 因此，返回的长度取决于该特定介质。 协议驱动程序可以使用仪表作为此返回的长度来确定的最大大小的数据包的微型端口驱动程序可能转发给协议驱动程序。 如果协议驱动程序预先分配缓冲区，它会相应地分配缓冲区。 返回的长度还指定了协议驱动程序可以将传递到的最大数据包[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)函数。

如果启用了一个 NIC 的微型端口驱动程序[802.1p 数据包优先级](https://msdn.microsoft.com/library/windows/hardware/ff562331)(微型端口驱动程序，即指定 NDIS\_MAC\_选项\_8021 P\_中的优先级位[OID\_GEN\_MAC\_选项](oid-gen-mac-options.md)OID 位掩码)，然后微型端口驱动程序必须指定其最大的数据包总长度为 4 个字节不会早于接收数据包的最大大小，或通过发送网络。 例如，如果 NIC 已启用的 802.1p 数据包优先级接收和发送数据包在网络上个 1514 字节的长度，NIC 的微型端口驱动程序必须为 1510 字节报告其最大的数据包总长度。 微型端口驱动程序必须永远不会指示绑定的协议驱动程序通过网络接收的数据包长度超过指定的 OID 的数据包大小最\_GEN\_最大\_总\_大小。 也就是说，即使微型端口驱动程序收到数据包通过网络不具有优先级值，但仍是基础中支持的最大大小，则微型端口驱动程序可能仅表示向上不超过大小的数据包指定的 OID\_GEN\_最大\_总\_大小。

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

## <a name="see-also"></a>另请参阅


[**NdisSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff564535)

[OID\_GEN\_MAC\_选项](oid-gen-mac-options.md)

 

 




