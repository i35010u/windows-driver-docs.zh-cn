---
title: OID_WAN_CO_GET_COMP_INFO
description: OID_WAN_CO_GET_COMP_INFO OID 请求微型端口驱动程序返回的功能信息的 nic 或其驱动程序，特别是是否为支持压缩。
ms.assetid: a2525548-ca5a-47a8-ab19-e0469913f6be
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_COMP_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e0af4684bfedf1be715ee6fa599dcaa74cc7b8df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564084"
---
# <a name="oidwancogetcompinfo"></a>OID\_WAN\_共同\_获取\_COMP\_信息


OID\_WAN\_共同\_获取\_COMP\_信息 OID 请求微型端口驱动程序返回的功能信息的 nic 或其驱动程序，特别是是否可以支持的压缩功能. 如果是这样，返回的值用于协商使用点对点协议 (PPP) 压缩控制协议的压缩。 协议随后协商 PPP 压缩方案与[OID\_WAN\_共同\_设置\_COMP\_信息](oid-wan-co-set-comp-info.md)请求。 此压缩信息是特定于虚拟连接 (VC)。

压缩信息返回在 NDIS\_WAN\_共同\_获取\_COMP\_信息结构，定义，如下所示：

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_COMP_INFO {
         OUT NDIS_WAN_COMPRESS_INFO SendCapabilities;
         OUT NDIS_WAN_COMPRESS_INFO RecvCapabilities;
    } NDIS_WAN_CO_GET_COMP_INFO,   *PNDIS_WAN_CO_GET_COMP_INFO;
```




此结构的成员包含下列信息：

<a href="" id="sendcapabilities"></a>**SendCapabilities**  
指定包含有关用于发送数据的压缩功能的信息的结构。

<a href="" id="recvcapabilities"></a>**RecvCapabilities**  
指定包含有关接收数据的压缩功能的信息的结构。

<a name="remarks"></a>备注
-------

有关详细信息的 NDIS\_WAN\_压缩\_信息结构，请参阅[OID\_WAN\_获取\_COMP\_信息](https://msdn.microsoft.com/library/windows/hardware/ff561202)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WAN\_GET\_COMP\_INFO](https://msdn.microsoft.com/library/windows/hardware/ff561202)

[OID\_WAN\_CO\_SET\_COMP\_INFO](oid-wan-co-set-comp-info.md)








