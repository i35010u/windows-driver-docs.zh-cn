---
title: WDI_TLV_LINK_QUALITY_BAR_MAP
description: WDI_TLV_LINK_QUALITY_BAR_MAP 是一种 TLV，其中包含信号质量到 Wi-Fi 信号强度条的映射。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LINK_QUALITY_BAR_MAP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 894588200dfa27cd0107508840ceeab42242ddef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820553"
---
# <a name="wdi_tlv_link_quality_bar_map"></a>WDI \_ TLV \_ 链接 \_ 质量 \_ 栏 \_ 映射


WDI \_ tlv \_ 链接 \_ 质量 \_ 栏 \_ 映射是一个 tlv，其中包含信号质量到 Wi-Fi 信号强度条的映射。

## <a name="tlv-type"></a>TLV 类型


0xD8

## <a name="length"></a>长度


WDI \_ 链接 \_ 质量 \_ 栏 \_ 地图 \_ 参数元素的数组大小 (以字节为单位) 。 数组必须包含1个或多个元素。

**注意**  WDI \_ 链接 \_ 质量 \_ 栏 \_ 地图 \_ 参数不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 类型                                         | 描述                                         |
|----------------------------------------------|-----------------------------------------------------|
| WDI \_ 链接 \_ 质量 \_ 栏 \_ 地图 \_ 参数\[\] | 信号强度栏映射参数的数组。 |

 

WDI \_ 链接 \_ 质量 \_ 栏 \_ 地图 \_ 参数由下列元素组成。

| 类型  | 描述                                                                  |
|-------|------------------------------------------------------------------------------|
| UINT8 | 当前信号强度栏 (0-100) 的下限链接质量。    |
| UINT8 | 当前信号强度栏的链接质量 (0-100) 的上限。 |
| UINT8 | 信号强度条形号。                                              |

 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

 




