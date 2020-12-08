---
title: WDI_TLV_SCAN_MODE
description: WDI_TLV_SCAN_MODE 是包含扫描模式参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SCAN_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 82be0d69af13f23ee5f5e76145a146a7a96cdf36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834177"
---
# <a name="wdi_tlv_scan_mode"></a>WDI \_ TLV \_ 扫描 \_ 模式


WDI \_ tlv \_ 扫描 \_ 模式是包含扫描模式参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x6

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                | 描述                                                                                                                                                                                                                       |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                               | 完整扫描过程应重复的次数。 如果此值设置为0，则在主机中止任务之前，应重复扫描。                                                                     |
| [**WDI \_ 扫描 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_type)       | 指定应执行的扫描的类型。 如果 \_ \_ 设置了 WDI 扫描类型 \_ "活动"，则设备必须只扫描活动通道。                                                                                                |
| UINT8                                               | 指定是否需要实时更新，并在找到时必须报告已发现的条目，并附带推荐的限制逻辑。 当 Microsoft 组件管理 BSS 列表缓存时，此值始终为 true。 |
| [**WDI \_ 扫描 \_ 触发器**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_trigger) | 指定扫描的触发器。                                                                                                                                                                                               |

 

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

 

