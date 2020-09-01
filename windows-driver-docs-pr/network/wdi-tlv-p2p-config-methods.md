---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS 是包含 Wi-fi 直接配置方法的 TLV。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CONFIG_METHODS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 31b94b844e4623e3b24f91f987e4471ab54d3aa7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208491"
---
# <a name="wdi_tlv_p2p_config_methods"></a>WDI \_ TLV \_ P2P \_ CONFIG \_ 方法


WDI \_ tlv \_ P2P \_ CONFIG \_ 方法是包含 wi-fi 直接配置方法的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xEB

## <a name="length"></a>Length


UINT16) 大小 (（以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | [**WDI \_ WPS \_ 配置 \_ 方法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)中定义的配置方法。 仅 PIN 显示、PIN 键盘和 WFDS 适用。 |

 

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

 

