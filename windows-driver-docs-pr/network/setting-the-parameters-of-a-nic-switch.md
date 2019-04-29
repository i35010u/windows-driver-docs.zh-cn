---
title: 设置 NIC 交换机的参数
description: 设置 NIC 交换机的参数
ms.assetid: 79B4B0B7-32AB-4AE4-ACD2-CE17C93573BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f2c7905c31b1ed1b406e8fd3f353f3bf922a45e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382898"
---
# <a name="setting-the-parameters-of-a-nic-switch"></a>设置 NIC 交换机的参数


基础驱动程序可以更改为支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器已创建一个 NIC 开关参数。 设置对象标识符 (OID) 的驱动程序问题的请求[OID\_NIC\_交换机\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451823)要更改这些参数。 仅微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 适配器处理此 OID 集请求。

基础驱动程序将发出此 OID 集请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)参数要使用的结构NIC 交换机上更改。 然后，该驱动程序初始化[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构的 OID 请求和集**InformationBuffer**成员添加到指针**NDIS\_NIC\_交换机\_参数**结构。

可以更改仅有限 NIC 开关的配置参数。 基础驱动程序指定要更改设置的以下成员的参数[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构：

-   **SwitchId**成员设置为其参数将会更改的 NIC 交换机的标识符。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 交换机*。 **SwitchId**成员必须设置为 NDIS\_默认\_交换机\_id。

     

-   合适的 NDIS\_NIC\_交换机\_参数\_*Xxx*\_设置已更改标志**标志**成员。 成员[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)可以只更改结构，如果相应 NDIS\_NIC\_交换机\_参数\_*Xxx*\_中 Ntddndis.h 定义已更改的标志。

-   成员[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构，它们分别对应于 NDIS\_NIC\_交换机\_参数\_*Xxx*\_设置已更改标志**标志**成员，设置与要更改的 NIC 交换机配置参数。

    **请注意**  仅从 Windows Server 2012 **SwitchName**的成员[ **NDIS\_NIC\_交换机\_参数** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构可以通过 OID 集请求的更改[OID\_NIC\_开关\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451823)。

     

当它收到的 OID 集请求，PF 微型端口驱动程序必须遵循这些准则[OID\_NIC\_交换机\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451823)

-   如果 PF 微型端口驱动程序可以应用所做的更改，而无需进行重新初始化的网络适配器，该驱动程序将更改应用到的硬件和完成 OID 请求使用 NDIS\_状态\_成功。

    如果返回此状态代码，则 NDIS 更新注册表中的 NIC 交换机配置信息。

-   如果 PF 微型端口驱动程序要求的网络适配器以应用所做的更改进行重新初始化，该驱动程序完成 OID 请求使用 NDIS\_状态\_REINIT\_必需。

    如果返回此状态代码，则 NDIS 还会更新注册表中的 NIC 交换机配置信息。 但是，以使所做的更改生效颁发 OID 集请求的基础驱动程序必须重新初始化的网络适配器。

    **请注意**  PF 微型端口驱动程序支持静态 NIC 创建和配置可以返回 NDIS\_状态\_REINIT\_必需以确保该适配器将重新初始化的新参数才能生效。

     

-   如果 PF 微型端口驱动程序不能应用所做的更改请求中 OID，它必须失败 OID 并返回相应的 NDIS\_状态\_*Xxx*代码。

    在这种情况下，NDIS 不会更新注册表中的 NIC 交换机配置信息。

 

 





