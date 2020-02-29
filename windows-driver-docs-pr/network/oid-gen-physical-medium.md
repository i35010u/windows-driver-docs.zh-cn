---
title: OID_GEN_PHYSICAL_MEDIUM
description: 作为查询，OID_GEN_PHYSICAL_MEDIUM OID 指定了 NIC 支持的物理介质的类型。
ms.assetid: 84d7231b-8af2-4bdb-8df5-37088767f708
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PHYSICAL_MEDIUM 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 88b5bbb2f2f084994939d95fabc8f557a7f57e3e
ms.sourcegitcommit: 69939496f6d5cb535aad2bd426ab2baa8d7b9051
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78178058"
---
# <a name="oid_gen_physical_medium"></a>OID\_GEN\_物理\_中型

作为查询，OID\_GEN\_物理\_中型 OID 指定 NIC 支持的物理介质的类型。 此 OID 本质上是[oid\_GEN\_支持\_](oid-gen-media-supported.md)的扩展。

## <a name="version-information"></a>版本信息

**请注意**，在 NDIS 6.0 和6.1 中支持此 OID  。 对于 NDIS 6.20 和更高版本，请使用[OID\_GEN\_物理\_中型\_例如](oid-gen-physical-medium-ex.md)

### <a name="remarks"></a>备注

NDIS 处理微型端口驱动程序的此 OID。 微型端口驱动程序在初始化过程中提供了物理媒体值。

微型端口驱动程序报告物理介质类型，以便将其物理介质与它们声明为支持在[OID\_GEN\_介质\_支持](oid-gen-media-supported.md)的 oid 查询的介质区分开来。 这些媒体类型作为以下系统定义的值的一个正确子集列出，这些值来自**NDIS\_物理\_中型**枚举：

**NdisPhysicalMediumUnspecified**物理介质不是上述介质。 例如，单向卫星源是未指定的物理介质。

**NdisPhysicalMediumWirelessLan**数据包通过符合802.11 接口的微型端口驱动程序通过无线 LAN 网络传输。 有关此接口的详细信息，请参阅。 [802.11 无线 LAN 微型端口驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff543933(v=vs.85))

**NdisPhysicalMediumCableModem**数据包通过基于 DOCSIS 的电缆网络进行传输。

**NdisPhysicalMediumPhoneLine**数据包是通过标准电话线传输的。
包括 HomePNA 介质。
**NdisPhysicalMediumPowerLine**数据包通过连接到电源分配系统的连线传输。

**NdisPhysicalMediumDSL**数据包通过数字用户线路（DSL）网络传输。
包括 ADSL 和 UADSL （G）。
**NdisPhysicalMediumFibreChannel**数据包通过光纤通道互连传输。

**NdisPhysicalMedium1394**数据包通过 IEEE 1394 总线传输。

**NdisPhysicalMediumWirelessWan**数据包通过无线 WAN 链接传输。 包括 CDPD、CDMA 和 GPRS。

<a href="" id="ndisphysicalmediumnative802-11"></a>**NdisPhysicalMediumNative802\_11**数据包通过符合本机802.11 接口的微型端口驱动程序通过无线 LAN 网络传输。 有关此接口的详细信息，请参阅[本机802.11 无线 LAN 微型端口驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff560648(v=vs.85))。

**请注意**，在 NDIS 6.0 和更高版本中支持本机802.11 接口  。

**NdisPhysicalMediumBluetooth**数据包通过蓝牙网络传输。 蓝牙是一种使用 2.4 GHz 频谱的短距离无线技术。

**NdisPhysicalMediumInfiniband**不能的物理介质。 数据包通过一种无法传输的互连传输。

**NdisPhysicalMediumUWB**Ultra 宽带（UWB）物理介质。 数据包通过 UWB 网络传输。 UWB 是一种射频平台，个人区域网络可以使用它以较高的速率在短距离之间进行无线通信。

<a href="" id="ndisphysicalmedium802-3"></a>**NdisPhysicalMedium802\_3**以太网（802.3）物理介质。 数据包通过符合802.3 接口规范的微型端口驱动程序通过有线 LAN 传输。 这种媒体类型不包括模拟802.3 的设备。

<a href="" id="ndisphysicalmedium802-5"></a>**NdisPhysicalMedium802\_5**令牌环物理介质。 （在 NDIS 6.0 和更高版本的驱动程序中不支持802.5。）数据包通过令牌环形网络通过符合802.5 接口规范的微型端口驱动程序传输。

**NdisPhysicalMediumIrda**红外（IrDA）物理介质。 数据包通过不可见的红外光红外光网络进行传输。

**NdisPhysicalMediumWiredWAN**有线的广域网（WAN）物理介质。 数据包通过有线 WAN 传输。

**NdisPhysicalMediumWiredCoWan**有线、面向连接的 WAN 物理介质。 数据包在面向连接的环境中通过有线 WAN 传输。

**NdisPhysicalMediumOther**物理介质不是上述介质。 **NdisPhysicalMediumOther**指定\_物理\_中型枚举中不存在的新物理中等类型。

NDIS 支持 OID\_GEN\_物理\_中型 OID，适用于支持较新网络的微型端口适配器，即使这些网络会传输显示到操作系统的数据包，并将其转换为标准和熟知良好的媒体类型。

较新的网络传输的数据包可能类似于标准介质，但可能具有新功能或与标准略有不同。 开发此 OID 是为了使上层驱动程序和应用程序能够确定 NIC 连接到的实际网络。 检索有关基础网络的信息后，上层驱动程序和应用程序可以使用此信息来修改此类驱动程序和应用程序的行为方式。

若要清楚地将 802.3 NIC 与未定义物理类型的仿真 802.3 NIC 区分开来，NDIS 6.0 及更高版本需要802.3 微型端口驱动程序来报告**NdisPhysicalMedium802\_3**。

### <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用<a href="oid-gen-physical-medium-ex.md" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM_EX](oid-gen-physical-medium-ex.md)">OID_GEN_PHYSICAL_MEDIUM_EX</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[支持 OID\_GEN\_介质\_](oid-gen-media-supported.md)

[OID\_代\_物理\_中型\_EX](oid-gen-physical-medium-ex.md)
