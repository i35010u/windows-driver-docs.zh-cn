---
title: WDI_TLV_P2P_DEVICE_INFO
description: WDI_TLV_P2P_DEVICE_INFO 是 TLV 包含 Wi-Fi Direct 设备信息。
ms.assetid: 6B68F334-4C21-4088-AD47-9EB41F9A1CB8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4e61453cab034cd04021aa4151560da2dc1ee950
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366339"
---
# <a name="wditlvp2pdeviceinfo"></a>WDI\_TLV\_P2P\_DEVICE\_INFO


WDI\_TLV\_P2P\_设备\_信息是包含 Wi-Fi Direct 设备信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x96

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                                                                                              |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_DEVICE\_INFO\_PARAMETERS**](wdi-tlv-p2p-device-info-parameters.md) |                                |          | 设备信息，包括 Wi-Fi Direct 设备地址、 受支持的配置方法和主要设备类型。 |
| [**WDI\_TLV\_P2P\_DEVICE\_NAME**](wdi-tlv-p2p-device-name.md)                        |                                |          | 此设备的设备名称。                                                                                         |

 

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

 

 




