---
title: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V4_PARAMETERS
description: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V4_PARAMETERS 是 OID_WDI_SET_ENCAPSULATION_OFFLOAD 用于指示是否应启动 IPv4 卸载 TLV。
ms.assetid: DC474D05-BF41-48F4-90CC-96C3B7F41ED0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V4_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9b0cb169cddebc1f46cf1403b2bd5502af7b1695
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543832"
---
# <a name="wditlvsetencapsulationoffloadv4parameters"></a>WDI\_TLV\_SET\_ENCAPSULATION\_OFFLOAD\_V4\_PARAMETERS


WDI\_TLV\_设置\_封装\_卸载\_V4\_参数是由 TLV [OID\_WDI\_设置\_封装\_卸载](https://msdn.microsoft.com/library/windows/hardware/dn925930)以指示是否应启动 IPv4 卸载。

## <a name="tlv-type"></a>TLV 类型


0xFD

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                             |
|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 指定是否应启动 IPv4 卸载。 此值设置为 NDIS\_卸载\_设置\_ON 如果启用，并且设置为 NDIS\_卸载\_设置\_关闭如果禁用了。 |

 

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

## <a name="see-also"></a>另请参阅


[**NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

 

 




