---
title: WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL
description: WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL 是指定的探测请求是否应包含在发现期间的侦听通道属性 TLV。
ms.assetid: 75662669-102A-4186-951C-58D1B36D1686
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6d6527d30c3e51ef78f209bb4a3455f5874a18bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392190"
---
# <a name="wditlvp2pincludelistenchannel"></a>WDI\_TLV\_P2P\_INCLUDE\_侦听\_通道


WDI\_TLV\_P2P\_INCLUDE\_侦听\_通道是指定的探测请求是否应包含在发现期间的侦听通道属性 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x128

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                                           |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 此参数指定的探测请求是否应包含在发现期间的侦听通道属性。 有效的值为的 0 （不包括） 和 1 （包括）。 |

 

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

 

 




