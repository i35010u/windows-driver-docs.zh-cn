---
title: OID_GEN_PHYSICAL_MEDIUM
description: 为查询，OID_GEN_PHYSICAL_MEDIUM OID 指定物理 NIC 支持的媒体的类型。
ms.assetid: 84d7231b-8af2-4bdb-8df5-37088767f708
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PHYSICAL_MEDIUM 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5627c37f1bef00ea906d4fa5f46f932898a6604b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555423"
---
# <a name="oidgenphysicalmedium"></a>OID\_GEN\_PHYSICAL\_MEDIUM


为查询，OID\_GEN\_物理\_中等 OID 指定的物理 NIC 支持的媒体类型。 此 OID 是实质上的扩展[OID\_代\_媒体\_支持](oid-gen-media-supported.md)。

**版本信息**

**请注意**  NDIS 6.0 和 6.1 中支持此 OID。 NDIS 6.20 和更高版本，使用[OID\_代\_物理\_中等\_EX](oid-gen-physical-medium-ex.md)。

 

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 的微型端口驱动程序。 微型端口驱动程序在初始化期间提供的物理介质的值。

微型端口驱动程序报告物理媒体类型以使其物理介质区别于声明它们中支持的媒体[OID\_代\_媒体\_支持](oid-gen-media-supported.md)OID 查询。 这些媒体类型被列为中的以下系统定义值的真子集**NDIS\_物理\_MEDIUM**枚举：

**NdisPhysicalMediumUnspecified**物理介质为 none 前面的媒介。 例如，单向附属源是未指定的物理介质。

**NdisPhysicalMediumWirelessLan**数据包通过符合的微型端口驱动程序通过无线 LAN 网络传输到 802.11 接口。 有关此接口的详细信息，请参阅。 [802.11 无线 LAN 微端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff543933)

**NdisPhysicalMediumCableModem**基于 DOCSIS 电缆网络上传输数据包。

**NdisPhysicalMediumPhoneLine**将通过标准电话线路传送数据包。
例如，包括 HomePNA 媒体。
**NdisPhysicalMediumPowerLine**数据包传输通过连接到配电系统的连接。

**NdisPhysicalMediumDSL**数字用户线 (DSL) 网络上传输数据包。
例如，包括，ADSL 和 UADSL (G.Lite)。
**NdisPhysicalMediumFibreChannel**数据包传输通过光纤通道互连。

**NdisPhysicalMedium1394**会通过 IEEE 1394 总线传输数据包。

**NdisPhysicalMediumWirelessWan**通过无线 WAN 链接传输数据包。 例如，包括，CDPD、 CDMA 和 GPRS。

<a href="" id="ndisphysicalmediumnative802-11"></a>**NdisPhysicalMediumNative802\_11**数据包通过符合的微型端口驱动程序通过无线 LAN 网络传输到本机 802.11 接口。 有关此接口的详细信息，请参阅[本机 802.11 无线 LAN 微端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff560648)。

**请注意**  NDIS 6.0 和更高版本和更高版本及更高版本中支持的本机 802.11 接口。

 

**NdisPhysicalMediumBluetooth**蓝牙网络上传输数据包。 蓝牙是使用 2.4 GHz 频谱的短程无线技术。

**NdisPhysicalMediumInfiniband**的 Infiniband 物理介质。 通过 infiniband 互连传输数据包。

**NdisPhysicalMediumUWB**超高宽带 (UWB) 物理介质。 UWB 网络上传输数据包。 UWB 是射频平台，供个人区域网可以用于以无线方式通信在短距离内以高的速度。

<a href="" id="ndisphysicalmedium802-3"></a>**NdisPhysicalMedium802\_3**以太网 (802.3) 物理介质。 数据包通过符合的微型端口驱动程序通过有线 LAN 传输到 802.3 接口规范。 此介质类型不包括模拟 802.3 的设备。

<a href="" id="ndisphysicalmedium802-5"></a>**NdisPhysicalMedium802\_5**令牌环物理介质。 （802.5 不支持 NDIS 6.0 和更高版本及更高版本的驱动程序中。）数据包通过符合的微型端口驱动程序通过令牌环网络传输到 802.5 接口规范。

**NdisPhysicalMediumIrda**红外 (IrDA) 物理介质。 不可见，红外浅范围 IrDA 网络上传输数据包。

**NdisPhysicalMediumWiredWAN**有线、 广域网 (wan) 物理介质。 有线 WAN 上传输数据包。

**NdisPhysicalMediumWiredCoWan**有线、 面向连接的 WAN 物理介质。 在面向连接的环境中有线 WAN 上传输数据包。

**NdisPhysicalMediumOther**物理介质为 none 前面的媒介。 **NdisPhysicalMediumOther**指定新的物理介质类型的 NDIS 中不存在\_物理\_中等枚举。

NDIS 支持 OID\_GEN\_物理\_支持较新的网络，即使这些网络传输到操作系统和作为标准的已知的 NDIS 的数据包的微型端口适配器的中等 OID媒体类型。

较新的网络传输的数据包，可能类似于标准介质，但可能包含新功能或从标准细微的差别。 此 OID 开发因此上层驱动程序和应用程序可以确定一个 NIC 连接到的实际网络。 检索有关基础网络的信息之后, 上层驱动程序和应用程序可以使用此信息来修改此类驱动程序和应用程序的行为方式。

以清楚地分开仿真 802.3 802.3 NIC NIC 为其是不存在定义的物理介质类型、 NDIS 6.0 和更高版本和更高版本及更高版本需要 802.3 微型端口驱动程序报告**NdisPhysicalMedium802\_3**.

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和 6.1 中受支持。 NDIS 6.20 和更高版本，使用<a href="oid-gen-physical-medium-ex.md" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM_EX](oid-gen-physical-medium-ex.md)">OID_GEN_PHYSICAL_MEDIUM_EX</a>相反。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_GEN\_媒体\_支持](oid-gen-media-supported.md)

[OID\_GEN\_PHYSICAL\_MEDIUM\_EX](oid-gen-physical-medium-ex.md)

 

 




