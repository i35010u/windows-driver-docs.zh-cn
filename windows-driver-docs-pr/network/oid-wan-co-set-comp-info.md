---
title: OID_WAN_CO_SET_COMP_INFO
description: OID_WAN_CO_SET_COMP_INFO OID 通知小型端口驱动程序所选的 PPP 压缩方案的微型端口驱动程序已使用 OID_WAN_CO_GET_COMP_INFO 查询返回的信息。
ms.assetid: f3b6b846-fa8c-425b-ba05-45927e744d66
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_SET_COMP_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a582a6d003e0989803eba8bfdf3de47c87e9cd55
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213303"
---
# <a name="oid_wan_co_set_comp_info"></a>OID \_ WAN \_ CO \_ 集 \_ 复合 \_ 信息


OID \_ wan \_ co \_ 集 \_ 复合 \_ 信息 OID 通知小型端口驱动程序所选的 PPP 压缩方案的微型端口驱动程序已使用 [OID \_ WAN \_ CO \_ 获取 \_ 复合 \_ 信息](oid-wan-co-get-comp-info.md) 查询返回的信息。 此 PPP 压缩方案特定于 (VC) 的虚拟连接。

协议为在 NDIS \_ WAN CO 集复合信息结构中选择的 PPP 压缩方案提供规范 \_ \_ \_ \_ ，定义如下：

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_SET_COMP_INFO {
         IN NDIS_WAN_COMPRESS_INFO SendCapabilities;
         IN NDIS_WAN_COMPRESS_INFO RecvCapabilities;
    } NDIS_WAN_CO_SET_COMP_INFO,   *PNDIS_WAN_CO_SET_COMP_INFO;
```




此结构的成员包含以下信息：

<a href="" id="sendcapabilities"></a>**SendCapabilities**  
指定一个结构，该结构包含有关用于发送数据的压缩功能的信息。

<a href="" id="recvcapabilities"></a>**RecvCapabilities**  
指定一个结构，该结构包含有关用于接收数据的压缩功能的信息。

<a name="remarks"></a>备注
-------

有关 NDIS \_ wan \_ 压缩信息结构的详细信息 \_ ，请参阅 [OID \_ wan \_ 获取 \_ 复合 \_ 信息](/previous-versions/windows/hardware/network/ff561202(v=vs.85))。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WAN \_ CO \_ 获取 \_ 复合 \_ 信息](oid-wan-co-get-comp-info.md)