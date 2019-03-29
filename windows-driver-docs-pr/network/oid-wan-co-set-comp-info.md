---
title: OID_WAN_CO_SET_COMP_INFO
description: OID_WAN_CO_SET_COMP_INFO OID 通知选择的微型端口驱动程序已返回信息与 OID_WAN_CO_GET_COMP_INFO 查询到的协议的 PPP 压缩方案的微型端口驱动程序。
ms.assetid: f3b6b846-fa8c-425b-ba05-45927e744d66
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_SET_COMP_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 574d3fcc2015278bd6fb41a9e9086fde02af3d30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567244"
---
# <a name="oidwancosetcompinfo"></a>OID\_WAN\_共同\_设置\_COMP\_信息


OID\_WAN\_共同\_设置\_COMP\_信息 OID 通知到的微型端口驱动程序已返回的信息与协议所选的PPP压缩方案的微型端口驱动程序[OID\_WAN\_共同\_获取\_COMP\_信息](oid-wan-co-get-comp-info.md)查询。 此 PPP 压缩方案是特定于虚拟连接 (VC)。

协议提供一个规范，则在 NDIS 中选取的 PPP 压缩方案用于\_WAN\_共同\_设置\_COMP\_信息结构，定义，如下所示：

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_SET_COMP_INFO {
         IN NDIS_WAN_COMPRESS_INFO SendCapabilities;
         IN NDIS_WAN_COMPRESS_INFO RecvCapabilities;
    } NDIS_WAN_CO_SET_COMP_INFO,   *PNDIS_WAN_CO_SET_COMP_INFO;
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


[OID\_WAN\_CO\_GET\_COMP\_INFO](oid-wan-co-get-comp-info.md)








