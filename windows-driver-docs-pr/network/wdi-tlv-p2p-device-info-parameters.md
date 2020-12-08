---
title: WDI_TLV_P2P_DEVICE_INFO_PARAMETERS
description: WDI_TLV_P2P_DEVICE_INFO_PARAMETERS 是包含 Wi-Fi 直接设备信息参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_INFO_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 782e8bfbb1314d36fc73509d7a7507150705e241
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823711"
---
# <a name="wdi_tlv_p2p_device_info_parameters"></a>WDI \_ TLV \_ P2P \_ 设备 \_ 信息 \_ 参数


WDI \_ tlv \_ P2P \_ 设备 \_ 信息 \_ 参数是包含 Wi-Fi 直接设备信息参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x86

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型       | 描述                                            |
|------------|--------------------------------------------------------|
| UINT8 \[ 6\] | 对等方的 Wi-Fi 直接设备地址。           |
| UINT16     | 设备支持的配置方法。     |
| UINT16     | 主要设备类型：主类型类别标识符。    |
| UINT8 \[ 4\] | 主要设备类型：分配给此设备类型的 OUI。 |
| UINT16     | 主要设备类型：子类别类型标识符。      |

 

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

 

 




