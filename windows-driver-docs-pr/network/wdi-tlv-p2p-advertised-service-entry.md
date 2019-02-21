---
title: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY 是包含一个播发的服务条目 TLV。
ms.assetid: C9BBA5D4-EC51-4D03-B997-A95B3168E64F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c4f317c9659282abaad0ac7833cf6b388dcdc8c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524114"
---
# <a name="wditlvp2padvertisedserviceentry"></a>WDI\_TLV\_P2P\_播发\_服务\_条目


WDI\_TLV\_P2P\_播发\_服务\_项是包含一个播发的服务条目 TLV。

## <a name="tlv-type"></a>TLV 类型


0xFC

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                           | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_SERVICE\_NAME**](wdi-tlv-p2p-service-name.md)               |                                |          | 中-8，最多 255 个字节的服务的名称。                                                                                                                          |
| [**WDI\_TLV\_P2P\_SERVICE\_NAME\_HASH**](wdi-tlv-p2p-service-name-hash.md)    |                                |          | 服务名称的哈希。                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_服务\_信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 此服务的服务信息。                                                                                                                                    |
| [**WDI\_TLV\_P2P\_SERVICE\_STATUS**](wdi-tlv-p2p-service-status.md)           |                                |          | 此服务的服务状态。                                                                                                                                          |
| [**WDI\_TLV\_P2P\_ADVERTISEMENT\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一地标识服务实例的 ID。                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | 配置方法中定义[ **WDI\_WPS\_配置\_方法**](https://msdn.microsoft.com/library/windows/hardware/dn898198)。 仅 PIN 显示、 PIN 键盘和 WFDS 均适用。 |

 

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

 

 




