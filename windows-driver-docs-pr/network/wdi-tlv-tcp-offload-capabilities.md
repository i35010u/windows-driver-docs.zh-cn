---
title: WDI_TLV_TCP_OFFLOAD_CAPABILITIES
description: WDI_TLV_TCP_OFFLOAD_CAPABILITIES 是 TLV 包含 TCP/IP 卸载功能。
ms.assetid: 9B3428CC-C9B4-4769-BD97-F25920C4AAF2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8844720123bae2835abf537242605c5bb7734064
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546699"
---
# <a name="wditlvtcpoffloadcapabilities"></a>WDI\_TLV\_TCP\_卸载\_功能


WDI\_TLV\_TCP\_卸载\_功能是包含 TCP/IP 卸载功能 TLV。

将报告功能值，如中所述[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567878)。 使用 NDIS\_卸载\_不\_支持和 NDIS\_卸载\_时，该值指示通过功能支持[OID\_WDI\_GET\_适配器\_功能](https://msdn.microsoft.com/library/windows/hardware/dn925838)。 对于 FIPS 模式下的连接，卸载 OFF 情况下处于状态下，用户设备。

## <a name="tlv-type"></a>TLV 类型


0xCA

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                         |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_CHECKSUM\_卸载\_功能**](wdi-tlv-checksum-offload-capabilities.md)                  |                                |          | 校验和卸载功能。      |
| [**WDI\_TLV\_LSO\_V1\_CAPABILITIES**](wdi-tlv-lso-v1-capabilities.md)                                      |                                |          | 大量发送卸载 V1 功能。 |
| [**WDI\_TLV\_LSO\_V2\_CAPABILITIES**](wdi-tlv-lso-v2-capabilities.md)                                      |                                |          | 大量发送卸载 V2 功能。 |
| [**WDI\_TLV\_RECEIVE\_COALESCE\_OFFLOAD\_CAPABILITIES**](wdi-tlv-receive-coalesce-offload-capabilities.md) |                                |          | 接收卸载功能。       |
| [**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md) |   |   | 指明是否卸载适用于 STA 端口仅或所有端口上。 当前适用于 802.11ad 仅适用于适配器。 |

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




