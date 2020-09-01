---
title: NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE
description: 支持 NDIS Service Service (QoS) 的微型端口驱动程序在首次解析其操作 NDIS QoS 参数或稍后更改时发出 NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 状态指示。
ms.assetid: 15D2B139-1AEA-4252-8599-0EA4ED2E3733
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6377116549f81648e7facf72151e026cb34f8ea5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207235"
---
# <a name="ndis_status_qos_operational_parameters_change"></a>NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改


支持 NDIS Service Service (QoS) 的微型端口驱动程序在其操作 NDIS QoS 参数首次解析或稍后更改时发出 **ndis \_ 状态 \_ QoS \_ 操作 \_ 参数 \_ 更改** 状态指示。 微型端口驱动程序用这些操作参数配置网络适配器，以执行 QoS 数据包传输。

当微型端口驱动程序发出此状态指示时，它会将[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员设置为指向[**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。 驱动程序用其操作的 NDIS QoS 参数初始化此结构。

**注意**   此 NDIS 状态指示仅对支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

小型端口驱动程序在以下条件下发出 **NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改** 状态指示：

-   微型端口驱动程序必须在最初解析其操作 NDIS QoS 参数并使用这些参数配置网络适配器之后发出 **NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改** 状态指示。

-   此初始状态指示后，微型端口驱动程序必须在其操作 NDIS QoS 参数发生更改时发出 **NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改** 状态指示。 如果更改了本地或远程 NDIS QoS 参数，就会发生这种情况。

-   小型端口驱动程序在数据中心桥接 (DCB) 组件时从 Windows 操作系统获取本地 NDIS QoS 参数 ( # A0) 发出对象标识符 (OID) oid [ \_ QoS \_ 参数](./oid-qos-parameters.md)的请求。 此 OID 请求包含用于指定本地 NDIS QoS 参数的 [**NDIS \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构。

    在某些情况下，微型端口驱动程序必须在解析其操作 NDIS QoS 参数时重写本地 NDIS QoS 参数。 如果本地 QoS 参数危害网络适配器上当前启用的任何基础协议或技术所使用的操作 QoS 参数，则更是如此。 例如，如果光纤通道通过以太网 (FCoE) 协议为网络适配器启用了远程启动，则驱动程序可以替代本地 QoS 参数。

    微型端口驱动程序通过发出 **ndis \_ 状态 \_ QoS \_ 操作 \_ 参数 \_ 更改** 状态指示，通知 NDIS 和过量驱动程序意图替代本地 NDIS QoS 参数。

    有关详细信息，请参阅 [管理 NDIS QoS 参数](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-qos--parameters)。

**注意**   过量驱动程序可以使用**ndis \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**状态指示来确定操作 NDIS QOS 参数。 此外，这些驱动程序还可以发出 oid [ \_ qos \_ 操作 \_ 参数](./oid-qos-operational-parameters.md) 的 oid 查询请求，以随时获取操作的 NDIS qos 参数。

 

有关微型端口驱动程序如何发出 **NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改** 状态指示的信息，请参阅 [指示对操作 NDIS QOS 参数的更改](./indicating-changes-to-the-operational-ndis-qos-parameters.md)。

有关各种类型的 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](./overview-of-ndis-qos-parameters.md)"。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)

[OID \_ QOS \_ 操作 \_ 参数](./oid-qos-operational-parameters.md)

 

