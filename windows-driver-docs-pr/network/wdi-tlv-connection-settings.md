---
title: WDI_TLV_CONNECTION_SETTINGS
description: WDI_TLV_CONNECTION_SETTINGS 是一个 TLV，其中包含 OID_WDI_TASK_CONNECT 的连接设置。
ms.assetid: E08E895D-BFD6-496E-82FE-881FDDB0B88E
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECTION_SETTINGS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 88676a88acf0b2e36277d865253b0aa45bc596ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843385"
---
# <a name="wdi_tlv_connection_settings"></a>WDI\_TLV\_连接\_设置


WDI\_TLV\_连接\_设置是一个 TLV，其中包含[OID\_WDI\_TASK\_连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-connect)的连接设置。

## <a name="tlv-type"></a>TLV 类型


0x3F

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                         | 描述                                                                                                                                                                                                               |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                                        | 指定这是首次连接请求（值为0）还是漫游连接（值为1）。                                                                                                                   |
| UINT8                                                        | 指定这是否是与具有隐藏/非广播 Ssid 的网络的连接。 连接到隐藏网络时，此值为1。                                                                                      |
| UINT8                                                        | 这会设置 dot11ExcludeUnencrypted MIB。 如果此值为 false （0），并且密码算法为 WEP，则端口必须连接到未在管理框中设置隐私字段的 Ap。                             |
| UINT8                                                        | 指定是否启用了 MFP （1）或禁用（0）。 当且仅当此值设置为1（已启用）时，工作站必须在关联请求中公布其 802.11 w 功能。                                          |
| UINT8                                                        | 指定是启用（1）还是禁用（0）主机 FIPS 模式。                                                                                                                                                               |
| [**WDI\_ASSOC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status)（UINT32） | 指定漫游所需的原因。 如果由于 NDIS\_状态而触发此情况[\_WDI\_指示\_漫游\_需要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)，这将包含漫游指示的原因。 |
| [**WDI\_漫游\_触发器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_roam_trigger)（UINT32） | 指定此漫游是否为重要漫游，因为 AP 已在其 BSS 转换请求操作框中设置了即将发生的解除。                                                                         |
| UINT8                                                        | 指定是否支持 802.11 v BSS 转换。 如果此位设置为1，则在关联请求中，工作站必须将扩展功能元素（位19）的 BSS 转换字段设置为1。                   |

 

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

 

 




