---
title: WDI_TLV_P2P_DEVICE_CAPABILITY
description: WDI_TLV_P2P_DEVICE_CAPABILITY 是 TLV 包含 Wi-Fi Direct 设备功能。
ms.assetid: 490CA066-998F-4F15-AFC2-028299042496
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_CAPABILITY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 86d861b334849837f3df3531b075a3d77f311654
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544716"
---
# <a name="wditlvp2pdevicecapability"></a>WDI\_TLV\_P2P\_设备\_功能


WDI\_TLV\_P2P\_设备\_功能是包含 Wi-Fi Direct 设备功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0x84

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT8  | 表 12 个 Wi-Fi Direct 技术规范中定义的 Wi-Fi Direct 设备功能的位图。            |
| UINT8  | 当前设置由操作系统在更高版本的设备功能位图中的 Wi-Fi Direct 功能的位图。 |
| UINT32 | 一个位掩码，指示启用哪些 WPS 版本。                                                                        |

 

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

 

 




