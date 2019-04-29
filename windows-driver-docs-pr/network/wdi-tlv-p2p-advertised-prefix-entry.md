---
title: WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY
description: WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY 是包含 Wi-Fi Direct TLV 播发前缀条目。
ms.assetid: 484A7784-EDD5-46F0-91E0-060D23ADC0BD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a4018c0eeb561d6963a43c14f37fe40252e8617e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383166"
---
# <a name="wditlvp2padvertisedprefixentry"></a>WDI\_TLV\_P2P\_播发\_前缀\_条目


WDI\_TLV\_P2P\_播发\_前缀\_项是包含 Wi-Fi Direct TLV 播发前缀条目。

## <a name="tlv-type"></a>TLV 类型


0x110

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                        | 允许多个 TLV 实例 | 可选 | 描述                                                      |
|-----------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_SERVICE\_NAME**](wdi-tlv-p2p-service-name.md)            |                                |          | 服务的名称，以 UTF – 8，最大大小为 255 个字节。 |
| [**WDI\_TLV\_P2P\_SERVICE\_NAME\_HASH**](wdi-tlv-p2p-service-name-hash.md) |                                |          | 服务名称的哈希。                                            |

 

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

 

 




