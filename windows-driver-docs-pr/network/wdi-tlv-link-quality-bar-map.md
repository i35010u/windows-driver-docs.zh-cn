---
title: WDI_TLV_LINK_QUALITY_BAR_MAP
description: WDI_TLV_LINK_QUALITY_BAR_MAP 是包含映射到的 Wi-fi 信号强度条的信号质量 TLV。
ms.assetid: 35E073F4-D372-466A-98FF-0AAB1695284E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LINK_QUALITY_BAR_MAP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ae8f9386f063b706ebd69bab342a3208b5c618a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564785"
---
# <a name="wditlvlinkqualitybarmap"></a>WDI\_TLV\_链接\_质量\_栏\_映射


WDI\_TLV\_链接\_质量\_栏\_映射是包含映射到的 Wi-fi 信号强度条的信号质量 TLV。

## <a name="tlv-type"></a>TLV 类型


0xD8

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_链接\_质量\_栏\_映射\_参数元素。 该数组必须包含一个或多个元素。

**请注意**  WDI\_链接\_质量\_栏\_映射\_参数不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                         | 描述                                         |
|----------------------------------------------|-----------------------------------------------------|
| WDI\_LINK\_QUALITY\_BAR\_MAP\_PARAMETERS\[\] | 栏将参数映射的信号强度的数组。 |

 

WDI\_链接\_质量\_栏\_映射\_参数包含以下元素。

| 在任务栏的搜索框中键入  | 描述                                                                  |
|-------|------------------------------------------------------------------------------|
| UINT8 | 质量越低限制链接 (0-100) 的当前的信号强度栏。    |
| UINT8 | 当前信号强度栏的链接质量 (0-100) 的上限。 |
| UINT8 | 信号强度栏数。                                              |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




