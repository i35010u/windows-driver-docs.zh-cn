---
title: WDI_TLV_PRIVACY_EXEMPTION_ENTRY
description: WDI_TLV_PRIVACY_EXEMPTION_ENTRY 是包含隐私例外条目 TLV。
ms.assetid: 086BD366-F54C-4BF4-8544-CC2AB2472EB2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PRIVACY_EXEMPTION_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a43f519cc1a9babd49bf80a3af2e4a150335cb38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366514"
---
# <a name="wditlvprivacyexemptionentry"></a>WDI\_TLV\_隐私\_免除\_条目


WDI\_TLV\_隐私\_免除\_项是包含隐私例外条目 TLV。

## <a name="tlv-type"></a>TLV 类型


0x48

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                   | 描述                                                 |
|------------------------------------------------------------------------|-------------------------------------------------------------|
| UINT16                                                                 | 指定 IEEE EtherType big endian 字节顺序。      |
| [**WDI\_免除\_操作\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type) | 指定例外的操作类型。                 |
| [**WDI\_免除\_数据包\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_exemption_packet_type) | 指定例外适用于的数据包的类型。 |

 

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

 

 




