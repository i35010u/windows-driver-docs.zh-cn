---
title: IPsec 卸载版本 2 简介
description: IPsec 卸载版本 2 简介
ms.assetid: d8fd0bf8-f7b6-44ad-a3dc-f10bb20ce651
keywords:
- 有关 IPsecOV2 IPsecOV2 WDK TCP/IP 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc1204bdbad0d7dd689eb0b21a050b78dc7c6e59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363013"
---
# <a name="introduction-to-ipsec-offload-version-2"></a>IPsec 卸载版本 2 简介

\[IPsec 任务卸载功能已弃用，不应使用。\]




IPsec 卸载版本 2 (IPsecOV2) 扩展中 IPsec 卸载版本 1 (IPsecOV1) 提供的服务。 有关 IPsecOV1 卸载和 IPsec 的详细信息，请参阅[IPsec 卸载版本 1](ipsec-offload-version-1.md)。

NDIS 6.1 和更高版本的微型端口驱动程序报告 IPsecOV2 卸载到 NDIS 的微型端口适配器的功能。 若要报告 IPsec 功能：

-   在初始化期间，微型端口驱动程序报告任务卸载默认配置和硬件功能的中的微型端口适配器[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)结构。

-   如果已配置的功能更改，微型端口驱动程序将报告使用的当前配置[ **NDIS\_状态\_任务\_卸载\_当前\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff567424)状态指示。 如果可以更改配置[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 设置微型端口适配器的当前任务卸载配置。 此外，如果下的硬件配置[MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)的更改，MUX 中间驱动程序必须报告使用的硬件配置更改[ **NDIS\_状态\_任务\_卸载\_硬件\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff567425)状态指示。

NDIS 报告到过量协议中的驱动程序卸载功能的微型端口适配器的默认配置[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构。 过量协议驱动程序可以选择的 IPsecOV2 任务卸载的服务的当前配置中支持的服务。 [ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状态指示确保所有的过量使用新的功能信息更新协议驱动程序。

在初始化期间报告的硬件功能，微型端口驱动程序必须从注册表中读取的标准化的关键字。 有关 IPsecOV2 卸载功能的详细信息，请参阅[报告 NIC 的 IPsec 卸载版本 2 功能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)。

**请注意**  NDIS NDIS 6.1 和更高版本的驱动程序提供直接的 OID 请求接口。 [直接 OID 请求路径](https://msdn.microsoft.com/library/windows/hardware/ff564736)支持查询或频繁设置的 OID 请求。

 

提供了 IPsecOV2 [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)， [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_更新\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569814)，并且[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)直接 OID 请求，以使协议驱动程序，以添加、 更新和删除安全关联 (Sa)。 有关 SAs 的详细信息，请参阅[IPsec 卸载版本 2 中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

NIC 可以执行 IPsec 卸载任务上发送和接收路径。 使用 NDIS 驱动程序[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565818)，[ **NDIS\_IPSEC\_卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff565812)，并[ **NDIS\_IPSEC\_卸载\_V2\_隧道\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565843)结构，以访问 IPsec 带外 (OOB) 信息。

在发送路径基础驱动程序将该句柄设置为 OOB 信息中的出站 SA 和 IPsec 标头信息[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，以指定应执行 NIC IPsecOV2 将任务卸载。

接收路径上 SA 卸载后，NIC 必须执行 IPsec 对匹配到 NDIS 微型端口驱动程序报告的功能的所有已接收数据包的处理。 微型端口驱动程序 OOB 信息中设置相应标志[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，以指定特定卸载 NIC 执行的任务和这些操作的结果。

详细信息大约发送和接收 IPsecOV2 中处理，请参阅[IPsec 卸载版本 2 发送网络数据](sending-network-data-with-ipsec-offload-version-2.md)并[IPsec 卸载版本 2 接收网络数据](receiving-network-data-with-ipsec-offload-version-2.md)。

 

 





