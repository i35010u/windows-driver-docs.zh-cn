---
title: WDI_TLV_CONNECTION_SETTINGS
description: WDI_TLV_CONNECTION_SETTINGS 是包含 OID_WDI_TASK_CONNECT 连接设置的 TLV。
ms.assetid: E08E895D-BFD6-496E-82FE-881FDDB0B88E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECTION_SETTINGS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e7b0f4308732563890187598f6a3148f5a6b40d7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212305"
---
# <a name="wdi_tlv_connection_settings"></a>WDI \_ TLV \_ 连接 \_ 设置


WDI \_ tlv \_ 连接 \_ 设置是一个 tlv，其中包含 [OID \_ WDI \_ TASK \_ CONNECT](./oid-wdi-task-connect.md)的连接设置。

## <a name="tlv-type"></a>TLV 类型


0x3F

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                         | 说明                                                                                                                                                                                                               |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                                        | 指定这是第一次连接请求 (值 0) 或 (值为 1) 的漫游连接。                                                                                                                   |
| UINT8                                                        | 指定这是否是与具有隐藏/非广播 Ssid 的网络的连接。 连接到隐藏网络时，此值为1。                                                                                      |
| UINT8                                                        | 这会设置 dot11ExcludeUnencrypted MIB。 如果此值为 false (0) 并且密码算法为 WEP，则端口必须连接到未在管理框架中设置隐私字段的 Ap。                             |
| UINT8                                                        | 指定是 (1) 还是禁用了 MFP (0) 。 当且仅当此值设置为 1 (启用) 时，工作站才能在关联请求中公布其 802.11 w 功能。                                          |
| UINT8                                                        | 指定是否启用了主机-FIPS 模式 (1) 或禁用 (0) 。                                                                                                                                                               |
| [**WDI \_ASSOC \_ 状态**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32)  | 指定漫游所需的原因。 如果这是由于 [NDIS \_ 状态 \_ WDI \_ 指示 \_ \_ 需要漫游](./ndis-status-wdi-indication-roaming-needed.md)引起的，这将包含漫游指示的原因。 |
| [**WDI \_ (UINT32) 漫游 \_ 触发器**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_roam_trigger) | 指定此漫游是否为重要漫游，因为 AP 已在其 BSS 转换请求操作框中设置了即将发生的解除。                                                                         |
| UINT8                                                        | 指定是否支持 802.11 v BSS 转换。 如果此位设置为1，则在关联请求中，工作站必须将扩展功能元素的 "BSS 转换" 字段 (位 19) 设置为1。                   |

 

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

 

