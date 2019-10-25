---
title: 设置 NIC 交换机的参数
description: 设置 NIC 交换机的参数
ms.assetid: 79B4B0B7-32AB-4AE4-ACD2-CE17C93573BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15832bd122143b09587454b51b0a334506c2eda3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841933"
---
# <a name="setting-the-parameters-of-a-nic-switch"></a>设置 NIC 交换机的参数


过量驱动程序可以更改在支持单根 i/o 虚拟化（SR-IOV）的网络适配器上创建的 NIC 交换机的参数。 驱动程序发出 OID\_NIC 的对象标识符（OID）设置请求[\_开关\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)更改这些参数。 只有 SR-IOV 适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序会处理此 OID 设置请求。

在过量驱动程序发出此 OID 集请求之前，它必须使用 NIC 交换机上要更改的参数来初始化[**NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 然后，该驱动程序将为 OID 请求初始化[**ndis\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，并将**InformationBuffer**成员设置为**NDIS\_NIC\_SWITCH\_参数**结构的指针。

只能更改 NIC 交换机的有限子集的配置参数。 过量驱动程序通过以下方法指定要更改的参数：设置\_NIC 的以下成员[ **\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构：

-   **SwitchId**成员设置为将更改其参数的 NIC 交换机的标识符。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 "*默认 NIC 交换机*"。 **SwitchId**成员必须设置为 NDIS\_默认\_交换机\_ID。

     

-   在**flags**成员中设置相应的 NDIS\_NIC\_交换机\_参数\_*Xxx*\_更改的标志。 仅当在 Ntddndis 中定义了相应的 NDIS\_NIC 时，才能更改[**NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构\_\_*Xxx*\_changed 标志.

-   [**Ndis\_nic 的成员\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构，该结构对应于 NDIS\_NIC\_switch\_ *\_\_* member，用要更改的 NIC 交换机配置参数进行设置。

    **请注意**  从 Windows Server 2012 开始，只能通过 OID\_NIC 的 oid 集请求来更改\_Nic 的**SWITCHNAME**成员[ **\_开关\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构[\_开关\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)。

     

当 PF [\_交换机\_参数接收 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)的 oid 设置请求时，PF 微型端口驱动程序必须遵循这些准则\_

-   如果 PF 微型端口驱动程序可以应用更改而无需重新初始化网络适配器，则驱动程序会将更改应用到硬件，并使用 NDIS\_状态完成 OID 请求，\_成功。

    如果返回此状态代码，NDIS 将更新注册表中的 NIC 交换机配置信息。

-   如果 PF 微型端口驱动程序需要重新初始化网络适配器以应用更改，则驱动程序将使用 NDIS\_状态完成 OID 请求，\_REINIT\_必需。

    如果返回此状态代码，NDIS 还会在注册表中更新 NIC 交换机配置信息。 但是，发出 OID 集请求的过量驱动程序必须重新初始化网络适配器，以使更改生效。

    **请注意**  PF 支持静态 NIC 创建和配置的微型端口驱动程序可以将 NDIS\_状态返回\_REINIT\_要求，以确保重新初始化适配器以使新参数生效。

     

-   如果 PF 微型端口驱动程序无法应用 OID 中请求的更改，则它必须使 OID 失败，并返回相应的 NDIS\_状态\_*Xxx*代码。

    在这种情况下，NDIS 不会更新注册表中的 NIC 交换机配置信息。

 

 





