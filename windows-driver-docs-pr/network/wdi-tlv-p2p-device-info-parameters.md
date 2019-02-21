---
title: WDI_TLV_P2P_DEVICE_INFO_PARAMETERS
description: WDI_TLV_P2P_DEVICE_INFO_PARAMETERS 是包含 Wi-Fi Direct 设备信息参数 TLV。
ms.assetid: A0B1AC85-5F99-4674-A1C4-E25554BDD89F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_INFO_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c34165d616b00bed68c2d78ad056b02cc696c0c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524599"
---
# <a name="wditlvp2pdeviceinfoparameters"></a>WDI\_TLV\_P2P\_DEVICE\_INFO\_PARAMETERS


WDI\_TLV\_P2P\_设备\_信息\_参数是包含 Wi-Fi Direct 设备信息参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x86

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                                            |
|------------|--------------------------------------------------------|
| UINT8\[6\] | Wi-Fi Direct 设备地址的对等方。           |
| UINT16     | 设备支持的配置方法。     |
| UINT16     | 主要设备类型：主要类型类别标识符。    |
| UINT8\[4\] | 主要设备类型：OUI 分配给此设备类型。 |
| UINT16     | 主要设备类型：类型的子类别标识符。      |

 

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

 

 




