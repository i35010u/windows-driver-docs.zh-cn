---
title: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY 是包含一个 ASP2 播发服务条目 TLV。
ms.assetid: CF7ED750-1987-4784-9E61-516EBBA22B9B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dc28299656dcd97578f3012b678b6ee28b94caea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356813"
---
# <a name="wditlvp2pasp2advertisedserviceentry"></a>WDI\_TLV\_P2P\_ASP2\_ADVERTISED\_SERVICE\_ENTRY


WDI\_TLV\_P2P\_ASP2\_播发\_服务\_项是包含一个 ASP2 播发服务条目 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12E

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                           | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_SERVICE\_TYPE**](wdi-tlv-p2p-service-type.md)               |                                |          | 服务类型的服务 (utf-8)，最多 21 字节。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_SERVICE\_TYPE\_HASH**](wdi-tlv-p2p-service-type-hash.md)    |                                |          | 服务类型的哈希值。                                                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_INSTANCE\_NAME**](wdi-tlv-p2p-instance-name.md)             |                                |          | 实例最多 63 个字节 (utf-8)，该服务的类型。                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_INSTANCE\_NAME\_HASH**](wdi-tlv-p2p-instance-name-hash.md)  |                                |          | "实例名称，服务类型"的哈希。                                                                                                                                                                                                                                                   |
| [**WDI\_TLV\_P2P\_服务\_信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 服务的服务信息。                                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_SERVICE\_STATUS**](wdi-tlv-p2p-service-status.md)           |                                |          | 服务的服务状态。                                                                                                                                                                                                                                                           |
| [**WDI\_TLV\_P2P\_ADVERTISEMENT\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一地标识服务实例的 ID。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | 配置方法中定义[ **WDI\_WPS\_配置\_方法**](https://msdn.microsoft.com/library/windows/hardware/dn898198)。 仅**WDI\_WPS\_配置\_方法\_显示**， **WDI\_WPS\_配置\_方法\_键盘**，并**WDI\_WPS\_配置\_方法\_WFDS\_默认**适用。 |

 

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

 

 




