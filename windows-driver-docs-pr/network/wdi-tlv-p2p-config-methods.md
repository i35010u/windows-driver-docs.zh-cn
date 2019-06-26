---
title: WDI_TLV_P2P_CONFIG_METHODS
description: WDI_TLV_P2P_CONFIG_METHODS 是 TLV 包含 Wi-Fi Direct 配置方法。
ms.assetid: 95F81FBB-CF78-47EC-8DB3-90F639C30865
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CONFIG_METHODS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b5e1d4c3807bc0cdf4f3303839bf9053b15790f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355104"
---
# <a name="wditlvp2pconfigmethods"></a>WDI\_TLV\_P2P\_CONFIG\_方法


WDI\_TLV\_P2P\_CONFIG\_方法是包含 Wi-Fi Direct 配置方法 TLV。

## <a name="tlv-type"></a>TLV 类型


0xEB

## <a name="length"></a>长度


UINT16 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 配置方法中定义[ **WDI\_WPS\_配置\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_wps_configuration_method)。 仅 PIN 显示、 PIN 键盘和 WFDS 均适用。 |

 

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

 

 




