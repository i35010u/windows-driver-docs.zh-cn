---
title: WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS
description: WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS 是包含网络列表卸载 (NLO) 参数的 OID_WDI_SET_NETWORK_LIST_OFFLOAD TLV。
ms.assetid: B8DD3BB6-DB90-4500-9BD5-252230F4BAAD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1a57cef35df6f346d947deec674c27b8b554e067
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392269"
---
# <a name="wditlvnetworklistoffloadparameters"></a>WDI\_TLV\_NETWORK\_LIST\_OFFLOAD\_PARAMETERS


WDI\_TLV\_网络\_列表\_卸载\_参数是包含网络列表卸载 (NLO) 参数 TLV [OID\_WDI\_集\_网络\_列表\_卸载](https://msdn.microsoft.com/library/windows/hardware/dn925933)。

## <a name="tlv-type"></a>TLV 类型


0x59

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                    | 允许多个 TLV 实例 | 可选 | 描述                                                                                  |
|-----------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_NETWORK\_LIST\_OFFLOAD\_CONFIG**](wdi-tlv-network-list-offload-config.md) |                                |          | 指定 NLO 配置。                                                                 |
| [**WDI\_TLV\_SSID\_OFFLOAD**](wdi-tlv-ssid-offload.md)                                 | X                              | X        | 指定将卸载 Ssid。 此元素不存在时，应停止固件 NLO 扫描。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




