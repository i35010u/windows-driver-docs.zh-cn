---
title: 设置 NIC 交换机的参数
description: 设置 NIC 交换机的参数
ms.assetid: 79B4B0B7-32AB-4AE4-ACD2-CE17C93573BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc53903941337c692f4cc1e1973f1593381ef59
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214422"
---
# <a name="setting-the-parameters-of-a-nic-switch"></a>设置 NIC 交换机的参数


过量驱动程序可以更改 NIC 交换机的参数，这些参数在支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器上创建。 驱动程序 (OID 发出对象标识符) 设置 [oid \_ NIC \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md) 的请求以更改这些参数。 只有 PCI Express (PCIe) 物理功能 () PF 的微型端口驱动程序才能处理此 OID 集请求。

在过量驱动程序发出此 OID 集请求之前，它必须使用 NIC 交换机上要更改的参数来初始化 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构。 然后，该驱动程序将为 OID 请求初始化 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构，并将 **InformationBuffer** 成员设置为 **NDIS \_ NIC \_ 交换机 \_ 参数** 结构的指针。

只能更改 NIC 交换机的有限子集的配置参数。 过量驱动程序通过设置 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构的以下成员来指定要更改的参数：

-   **SwitchId**成员设置为将更改其参数的 NIC 交换机的标识符。

    **注意**   从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 " *默认 NIC 交换机*"。 **SwitchId**成员必须设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

     

-   在 \_ \_ flags 成员中设置相应的 NDIS NIC 交换机 \_ 参数 \_ *Xxx* \_ 更改**Flags**标志。 仅当在 Ntddndis 中定义了相应的 NDIS nic 交换机[** \_ \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) \_ \_ \_ 参数 \_ *Xxx* \_ changed 标志时，才能更改 NDIS nic 交换机参数结构的成员。

-   [**Ndis \_ nic \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的成员（该结构对应于 \_ \_ \_ flags 成员中已更改的 ndis nic 交换机参数 XXX）已 \_ *Xxx* \_ 设置为要更改的 NIC 交换机配置参数。 **Flags**

    **注意**   从 Windows Server 2012 开始，只能通过 oid [ \_ nic \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md)的 oid 集请求更改[**NDIS \_ nic \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的**SwitchName**成员。

     

当 PF 微型端口驱动程序收到[oid \_ NIC \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md)的 oid 集请求时，必须遵循这些指南

-   如果 PF 微型端口驱动程序可以应用更改而无需重新初始化网络适配器，则驱动程序会将更改应用到硬件，并完成具有 NDIS 状态成功的 OID 请求 \_ \_ 。

    如果返回此状态代码，NDIS 将更新注册表中的 NIC 交换机配置信息。

-   如果 PF 微型端口驱动程序需要重新初始化网络适配器以应用更改，则驱动程序将完成 OID 请求，并要求使用 NDIS \_ 状态 \_ REINIT \_ 。

    如果返回此状态代码，NDIS 还会在注册表中更新 NIC 交换机配置信息。 但是，发出 OID 集请求的过量驱动程序必须重新初始化网络适配器，以使更改生效。

    **注意**   支持静态 NIC 创建和配置的 PF 微型端口驱动程序可以返回 NDIS \_ 状态 REINIT，这 \_ \_ 是为了确保重新初始化适配器以使新参数生效。

     

-   如果 PF 微型端口驱动程序无法应用 OID 中请求的更改，则它必须使 OID 失败，并返回相应的 NDIS \_ 状态 \_ *Xxx*代码。

    在这种情况下，NDIS 不会更新注册表中的 NIC 交换机配置信息。

 

