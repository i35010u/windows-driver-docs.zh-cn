---
title: WDI_TLV_P2P_DEVICE_ADDRESS
description: WDI_TLV_P2P_DEVICE_ADDRESS 是包含组所有者的设备地址 TLV。
ms.assetid: EAC1972E-3D9B-4248-BAC3-3C2EB15D6817
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 99efe33e2d584128a8ff86091b6413553a91bee1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564701"
---
# <a name="wditlvp2pdeviceaddress"></a>WDI\_TLV\_P2P\_DEVICE\_ADDRESS


WDI\_TLV\_P2P\_设备\_地址是包含组所有者的设备地址 TLV。

## <a name="tlv-type"></a>TLV 类型


0x91

## <a name="length"></a>长度


大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://msdn.microsoft.com/library/windows/hardware/dn926071)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                            |
|---------------------------------------------------|----------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 组所有者的设备地址。 |

 

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

 

 




