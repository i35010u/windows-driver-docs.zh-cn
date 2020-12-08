---
title: WDI_TLV_BSS_ENTRY_SIGNAL_INFO
description: WDI_TLV_BSS_ENTRY_SIGNAL_INFO 为 TLV，其中包含 BSS 条目的信号信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_SIGNAL_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b650d4c0389d1feabe203abfdc35b845047096b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792605"
---
# <a name="wdi_tlv_bss_entry_signal_info"></a>WDI \_ TLV \_ BSS \_ 输入 \_ 信号 \_ 信息


WDI \_ tlv \_ bss \_ 输入 \_ 信号 \_ 信息是一个 tlv，其中包含 BSS 条目的信号信息。

## <a name="tlv-type"></a>TLV 类型


0xB

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                                        |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| INT32  | 收到的信号强度指示器 (对等方发出的信号或探测响应的 RSSI) 值。 此值是以分贝引用的单位（1.0 毫瓦 (dBm）来指定的)  |
| UINT32 | 由介于0到100之间的值指定的链接质量。 值100指定最高的链接质量。                                                                            |

 

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

 

 




