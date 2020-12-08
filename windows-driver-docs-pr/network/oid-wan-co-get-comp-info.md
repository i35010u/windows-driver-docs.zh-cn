---
title: OID_WAN_CO_GET_COMP_INFO
description: OID_WAN_CO_GET_COMP_INFO OID 请求微型端口驱动程序返回有关 NIC 或其驱动程序的功能的信息，特别是是否支持压缩。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_COMP_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9782ddf5b05688e89d2c5d7111cd910fabc50ea4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786059"
---
# <a name="oid_wan_co_get_comp_info"></a>OID \_ WAN \_ CO \_ 获取 \_ 复合 \_ 信息


OID \_ WAN \_ CO \_ 获取 \_ 复合 \_ 信息 OID 请求微型端口驱动程序返回有关 NIC 或其驱动程序的功能的信息，特别是是否支持压缩。 如果是这样，则返回的值用于与点对点协议 (PPP) Compression 控制协议的压缩进行协商。 协议随后使用 [OID \_ WAN \_ CO \_ 集 \_ 复合 \_ 信息](oid-wan-co-set-comp-info.md) 请求来协商 PPP 压缩方案。 此压缩信息特定于 (VC) 的虚拟连接。

在 NDIS \_ WAN \_ CO \_ 获取复合信息结构中返回压缩信息 \_ \_ ，如下所示：

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_COMP_INFO {
         OUT NDIS_WAN_COMPRESS_INFO SendCapabilities;
         OUT NDIS_WAN_COMPRESS_INFO RecvCapabilities;
    } NDIS_WAN_CO_GET_COMP_INFO,   *PNDIS_WAN_CO_GET_COMP_INFO;
```




此结构的成员包含以下信息：

<a href="" id="sendcapabilities"></a>**SendCapabilities**  
指定一个结构，该结构包含有关用于发送数据的压缩功能的信息。

<a href="" id="recvcapabilities"></a>**RecvCapabilities**  
指定一个结构，该结构包含有关用于接收数据的压缩功能的信息。

<a name="remarks"></a>备注
-------

有关 NDIS \_ wan \_ 压缩信息结构的详细信息 \_ ，请参阅 [OID \_ wan \_ 获取 \_ 复合 \_ 信息](/previous-versions/windows/hardware/network/ff561202(v=vs.85))。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WAN \_ 获取 \_ 复合 \_ 信息](/previous-versions/windows/hardware/network/ff561202(v=vs.85))

[OID \_ WAN \_ CO \_ 集 \_ 复合 \_ 信息](oid-wan-co-set-comp-info.md)
