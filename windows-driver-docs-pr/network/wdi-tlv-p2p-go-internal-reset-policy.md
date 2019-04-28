---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 是 TLV，其中包含有关操作通道选择 Wi-Fi Direct 转重置为已停止/重新启动后使用固件的策略。
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d0b49aed8609cee6d92ce59ecf1091ffed9d381f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329725"
---
# <a name="wditlvp2pgointernalresetpolicy"></a>WDI\_TLV\_P2P\_GO\_INTERNAL\_RESET\_POLICY


WDI\_TLV\_P2P\_转\_内部\_重置\_策略是包含有关操作通道选择停止 Wi-Fi Direct 转置后使用固件的策略 TLV /重新启动。

## <a name="tlv-type"></a>TLV 类型


0xB2

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                            | 描述                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_GO\_INTERNAL\_RESET\_POLICY**](https://msdn.microsoft.com/library/windows/hardware/dn926096) (UINT32) | 如果 Wi-Fi Direct 转重置为已停止/重新启动由 IHV 组件本身 （例如，对于蓝牙共同 ex 空间流降级），此配置将定义的固件操作后重置通道选择要采用的策略。 |

 

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

 

 




