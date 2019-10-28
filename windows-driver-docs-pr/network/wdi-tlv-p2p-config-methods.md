---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS 是包含 Wi-fi 直接配置方法的 TLV。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CONFIG_METHODS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a970603ab40ea577bbcf14afc5935d0c69a7df17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840455"
---
# <a name="wdi_tlv_p2p_config_methods"></a>WDI\_TLV\_P2P\_CONFIG\_方法


WDI\_TLV\_P2P\_CONFIG\_方法是包含 Wi-fi 直接配置方法的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xEB

## <a name="length"></a>长度


UINT16 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | WDI 中定义的配置方法[ **\_WPS\_配置\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)。 仅 PIN 显示、PIN 键盘和 WFDS 适用。 |

 

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

 

 




