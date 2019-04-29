---
title: WDI_TLV_BSSID_INFO
description: WDI_TLV_BSSID_INFO 是包含 BSSID 信息 TLV。
ms.assetid: C9E2B2D5-16CA-438D-AD86-1FA4F4F11CD1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSSID_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 80bc47d204ad03a02f4773b4b142aac491b797f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376237"
---
# <a name="wditlvbssidinfo"></a>WDI\_TLV\_BSSID\_INFO


WDI\_TLV\_BSSID\_信息是包含 BSSID 信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x120

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                                                                                                                                                                                                               |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 亚太可访问性。 有效值为 1 （不可访问），2 （未知） 和 3 （可访问）。                                                                                                                                                                                                                                                      |
| UINT8 | 安全性。 如果此值设置为 1，它指示此 BSSID 由标识 AP 支持相同的安全设置由在其当前关联 STA。 如果此值设置为 0，则指示的此应用程序不支持同一个安全预配、 或的安全信息目前不可用。 |
| UINT8 | 键范围位。 如果设置为 1，它表示指示此 BSSID AP 具有相同的验证器作为 AP 发送报表。 如果此位设置为 0，它表示一个不同的身份验证器或信息不可用。                                                                                                |
| UINT8 | 如果 dot11SpectrumManagementRequired 为 true，这是设置为 1。                                                                                                                                                                                                                                                                              |
| UINT8 | 如果 dot11QosOptionImplemented 为 true，这是设置为 1。                                                                                                                                                                                                                                                                                    |
| UINT8 | AP APSD 子字段设置为 1 的功能信息字段中时 dot11APSDOptionImplemented 为 true，并将其设置为 0 否则。                                                                                                                                                                                            |
| UINT8 | 如果 dot11RadioMeasurementActivated 为 true，这是设置为 1。                                                                                                                                                                                                                                                                               |
| UINT8 | 如果 dot11DelayedBlockAckOptionImplemented 为 true，这是设置为 1。                                                                                                                                                                                                                                                                        |
| UINT8 | 如果 dot11ImmediateBlockAckOptionImplemented 为 true，这是设置为 1。                                                                                                                                                                                                                                                                      |
| UINT8 | 如果表示此 BSSID AP 包括 MDE 其信息帧中，这是设置为 1。                                                                                                                                                                                                                                                |
| UINT8 | 这是设置为 1 以指示表示此 BSSID AP HT AP，包括其信号中的超线程功能元素。                                                                                                                                                                                                      |

 

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

 

 




