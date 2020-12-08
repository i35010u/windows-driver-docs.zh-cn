---
title: WDI_TLV_P2P_DEVICE_INFO
description: WDI_TLV_P2P_DEVICE_INFO 是包含 Wi-Fi 直接设备信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 660a9896d79798032589a14a0050b0b1cc3ac600
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823709"
---
# <a name="wdi_tlv_p2p_device_info"></a>WDI \_ TLV \_ P2P \_ 设备 \_ 信息


WDI \_ tlv \_ P2P \_ 设备 \_ 信息是包含 Wi-Fi 直接设备信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x96

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                  | 允许多个 TLV 实例 | 可选 | 说明                                                                                                              |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 信息 \_ 参数**](wdi-tlv-p2p-device-info-parameters.md) |                                |          | 设备信息，包括 Wi-Fi 直接设备地址、支持的配置方法和主要设备类型。 |
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 名称**](wdi-tlv-p2p-device-name.md)                        |                                |          | 此设备的设备名称。                                                                                         |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




