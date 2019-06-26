---
title: WDI_TLV_SCAN_MODE
description: WDI_TLV_SCAN_MODE 是包含扫描模式参数 TLV。
ms.assetid: 9F954B66-4F1D-48F2-9316-BE623DF0CAE6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SCAN_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b9c79939f2e99e5bbd5420be20070532f81010d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366505"
---
# <a name="wditlvscanmode"></a>WDI\_TLV\_扫描\_模式


WDI\_TLV\_扫描\_模式是包含扫描模式参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x6

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                | 描述                                                                                                                                                                                                                       |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                               | 完全扫描过程均应重复次数。 如果此值设置为 0，直到任务中止主机应重复扫描。                                                                     |
| [**WDI\_扫描\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_scan_type)       | 指定应执行的扫描类型。 如果 WDI\_扫描\_类型\_设置处于活动状态时，设备必须仅扫描活动通道。                                                                                                |
| UINT8                                               | 指定是否需要实时更新以及何时找到它们，与上面的建议限制逻辑必须报告发现的条目。 当 Microsoft 组件管理 BSS 列表缓存时，此值始终为 true。 |
| [**WDI\_扫描\_触发器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_scan_trigger) | 指定扫描的触发器。                                                                                                                                                                                               |

 

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

 

 




