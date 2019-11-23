---
title: NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE
description: 支持 NDIS 服务质量（QoS）的微型端口驱动程序会在其操作 NDIS QoS 参数首次解析或稍后更改时发出 NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 状态指示。
ms.assetid: 15D2B139-1AEA-4252-8599-0EA4ED2E3733
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9e537e9f05b1705aa252503b880e5ec670e1a7e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843530"
---
# <a name="ndis_status_qos_operational_parameters_change"></a>NDIS\_状态\_QOS\_操作\_参数\_更改


支持 NDIS 服务质量（QoS）的微型端口驱动程序会在以下情况中发出**ndis\_状态\_QoS\_运行\_参数\_更改**状态指示。 微型端口驱动程序用这些操作参数配置网络适配器，以执行 QoS 数据包传输。

当微型端口驱动程序发出此状态指示时，它会将[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员设置为指向[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。 驱动程序用其操作的 NDIS QoS 参数初始化此结构。

**请注意**  此 NDIS 状态指示仅对支持 IEEE 802.1 数据中心桥接（DCB）接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

在以下条件下，微型端口驱动程序会在 **\_QOS\_操作\_参数\_更改**状态指示中发出 NDIS\_状态：

-   微型端口驱动程序必须在 **\_QOS\_运行\_参数时发出 NDIS\_状态，\_更改**状态指示，然后在其最初解析其操作 NDIS QOS 参数并配置网络适配器。

-   在此初始状态指示后，微型端口驱动程序必须在运行的 NDIS QoS 参数发生更改时 **\_QOS\_操作\_\_参数发出 NDIS\_状态**。 如果更改了本地或远程 NDIS QoS 参数，就会发生这种情况。

-   当数据中心桥接（DCB）组件（Msdcb）发出 OID 的对象标识符（OID）方法请求[\_QoS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)时，微型端口驱动程序将从 Windows 操作系统获取本地 NDIS QoS 参数。 此 OID 请求包含一个[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，用于指定本地 NDIS QOS 参数。

    在某些情况下，微型端口驱动程序必须在解析其操作 NDIS QoS 参数时重写本地 NDIS QoS 参数。 如果本地 QoS 参数危害网络适配器上当前启用的任何基础协议或技术所使用的操作 QoS 参数，则更是如此。 例如，如果光纤通道通过以太网（FCoE）协议为网络适配器启用了远程启动，则驱动程序可以替代本地 QoS 参数。

    微型端口驱动程序通过发出**ndis\_状态\_QoS\_操作\_参数\_更改**状态指示，通知 ndis 和过量驱动程序的意图替代本地 NDIS QoS 参数。

    有关详细信息，请参阅[管理 NDIS QoS 参数](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-qos--parameters)。

**请注意**  过量驱动程序可以使用**NDIS\_状态\_QOS\_操作\_参数\_更改**状态指示来确定操作 NDIS QOS 参数。 此外，这些驱动程序还可以[\_QOS\_操作\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)发出 oid 查询请求，以便随时获取操作的 NDIS QOS 参数。

 

有关微型端口驱动程序如何发出**NDIS\_状态的信息\_QOS\_操作\_参数\_更改**状态指示，请参阅[指示对操作 NDIS QOS 参数的更改](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-changes-to-the-operational-ndis-qos-parameters)。

有关各种类型的 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)"。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)

[OID\_QOS\_操作\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)

 

 




