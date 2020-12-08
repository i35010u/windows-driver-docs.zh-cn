---
title: OID_GEN_RNDIS_CONFIG_PARAMETER
description: 作为集，OID_GEN_RNDIS_CONFIG_PARAMETER 用于设置特定于设备的参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RNDIS_CONFIG_PARAMETER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9a7adfece53265e72a9c040c2ed29aca06391406
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798005"
---
# <a name="oid_gen_rndis_config_parameter"></a>OID \_ GEN \_ RNDIS \_ CONFIG \_ 参数


作为集，OID \_ GEN \_ RNDIS \_ CONFIG \_ 参数用于设置特定于设备的参数。 该主机仅将它用于 RNDIS 设备。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 RNDIS 设备。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

OID \_ GEN \_ RNDIS \_ CONFIG \_ 参数用于 RNDIS 设备。 主机使用它来设置特定于设备的参数。 它不由微型端口驱动程序使用。 有关此 OID 的详细信息，请参阅 [设置 Device-Specific 参数](./setting-device-specific-parameters.md)。

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

 

