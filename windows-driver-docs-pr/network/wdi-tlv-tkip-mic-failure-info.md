---
title: WDI_TLV_TKIP_MIC_FAILURE_INFO
description: WDI_TLV_TKIP_MIC_FAILURE_INFO 是包含 TKIP-MIC 故障信息的 TLV。
ms.assetid: BBF168BE-6223-4C54-AFF5-17878D07EFBD
ms.date: 07/18/2017
keywords:
- WDI_TLV_TKIP_MIC_FAILURE_INFO 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0c1734d4dcc6f702bc19107a6a0bdaef1a05a981
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841723"
---
# <a name="wdi_tlv_tkip_mic_failure_info"></a>WDI\_TLV\_TKIP\_MIC\_故障\_信息


WDI\_TLV\_TKIP\_MIC\_故障\_INFO 是包含 TKIP-MIC 故障信息的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x57

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                                                                                              |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定哪个密码密钥类型检测到 TKIP-MIC 发生故障。 如果该值为1，则会通过默认密码密钥检测到 TKIP-MIC 故障。 如果此值为0，则通过密钥映射密码密钥检测到 TKIP-MIC 故障。 |
| UINT32                                            | 指定默认键数组中的密码键的索引。 有效值范围为0到3。                                                                                                                                                   |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定传输失败麦克风验证的数据包的对等节点的 MAC 地址。                                                                                                                                                          |

 

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
<td><p>Windows 10</p></td>
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

 

 




