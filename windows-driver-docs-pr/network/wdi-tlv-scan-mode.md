---
title: WDI_TLV_SCAN_MODE
description: WDI_TLV_SCAN_MODE 是包含扫描模式参数的 TLV。
ms.assetid: 9F954B66-4F1D-48F2-9316-BE623DF0CAE6
ms.date: 07/18/2017
keywords:
- WDI_TLV_SCAN_MODE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f22f52d952e4a8761417810f744f618d2cd8c94e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841738"
---
# <a name="wdi_tlv_scan_mode"></a>WDI\_TLV\_扫描\_模式


WDI\_TLV\_SCAN\_模式是包含扫描模式参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x6

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                | 描述                                                                                                                                                                                                                       |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                               | 完整扫描过程应重复的次数。 如果此值设置为0，则在主机中止任务之前，应重复扫描。                                                                     |
| [**WDI\_扫描\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_type)       | 指定应执行的扫描的类型。 如果已设置 ACTIVE\_扫描\_类型\_活动状态，则设备必须仅扫描活动通道。                                                                                                |
| UINT8                                               | 指定是否需要实时更新，并在找到时必须报告已发现的条目，并附带推荐的限制逻辑。 当 Microsoft 组件管理 BSS 列表缓存时，此值始终为 true。 |
| [**WDI\_扫描\_触发器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_trigger) | 指定扫描的触发器。                                                                                                                                                                                               |

 

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
<td><p>Windows 10</p></td>
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

 

 




