---
title: WDI_TLV_TKIP_MIC_FAILURE_INFO
description: WDI_TLV_TKIP_MIC_FAILURE_INFO 是包含 TKIP-MIC 故障信息的 TLV。
ms.assetid: BBF168BE-6223-4C54-AFF5-17878D07EFBD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TKIP_MIC_FAILURE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d2463848febc49402677925bec5ee41cf6565a77
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208469"
---
# <a name="wdi_tlv_tkip_mic_failure_info"></a>WDI \_ TLV \_ TKIP \_ MIC \_ 故障 \_ 信息


WDI \_ tlv \_ TKIP \_ mic \_ 故障信息 \_ 是包含 TKIP-MIC 故障信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x57

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                                                                                                                                                                                                                              |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定哪个密码密钥类型检测到 TKIP-MIC 发生故障。 如果该值为1，则会通过默认密码密钥检测到 TKIP-MIC 故障。 如果此值为0，则通过密钥映射密码密钥检测到 TKIP-MIC 故障。 |
| UINT32                                            | 指定默认键数组中的密码键的索引。 有效值范围为0到3。                                                                                                                                                   |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定传输失败麦克风验证的数据包的对等节点的 MAC 地址。                                                                                                                                                          |

 

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

 

