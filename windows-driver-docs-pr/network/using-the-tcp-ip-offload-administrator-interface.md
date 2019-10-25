---
title: 使用 TCP/IP 卸载管理员界面
description: 使用 TCP/IP 卸载管理员界面
ms.assetid: 2418e577-17cd-4db7-adb0-44b705e29d38
keywords:
- TCP/IP 卸载 WDK 网络，管理员界面
- 卸载 WDK TCP/IP 传输，管理员界面
- 任务卸载 WDK TCP/IP 传输，管理员界面
- 连接卸载 WDK TCP/IP 传输，管理员界面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd4df27dadc5085d96df98dd29f69986314a16e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842967"
---
# <a name="using-the-tcpip-offload-administrator-interface"></a>使用 TCP/IP 卸载管理员界面





在 NDIS 6.0 和更高版本中，用户模式应用程序（或过量驱动程序）可以启用或禁用 TCP/IP 卸载功能。 系统管理员可以通过 Microsoft Windows Management Instrumentation （WMI）界面访问这些设置。 还可能会通过注册表设置禁用这些功能，如果硬件支持这些设置，则可以启用这些设置。

为了响应[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)对象标识符（OID）设置请求，微型端口驱动程序使用[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构中的设置来设置当前卸载或已卸载微型端口适配器的配置。

NDIS 在卸载标准化关键字的注册表中保留请求的设置。 当 NDIS 重新启动微型端口适配器时，微型端口驱动程序将读取卸载标准化关键字，并使用它们来设置 NIC 的默认卸载配置。 如果微型端口驱动程序还支持非标准关键字，则微型端口驱动程序会在更改任务卸载设置时负责更新注册表。 有关标准化关键字的详细信息，请参阅[网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

微型端口驱动程序必须使用[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构的内容来更新当前报告的卸载配置。 微型端口驱动程序必须报告当前配置，其中包含任务卸载[**ndis\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)或连接卸载 NDIS\_状态\_卸载\_恢复状态指示。 （有关 NDIS\_状态的信息\_卸载\_恢复，请参阅[ndis 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。）状态指示可确保所有的过量协议驱动程序都用新功能信息进行更新。

在用户模式应用程序（或过量驱动程序）设置[oid 之前\_tcp\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)它们可以使用[oid\_tcp\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 或[oid\_tcp\_连接\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)OID，以确定微型端口适配器的硬件可支持哪些功能。 使用 OID\_TCP\_卸载\_参数 OID 启用[OID\_tcp\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID 或 OID\_\_\_@no__t_ [当前未启用12_ 当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config) OID 报告。

如果硬件功能发生变化（例如，因为 MUX 中间驱动程序切换到差异底层微型端口适配器），则中间驱动程序必须使用 NDIS\_状态报告卸载硬件功能中的任何更改[ **\_任务\_卸载\_硬件\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)或[**NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-tcp-connection-offload-hardware-capabilities)状态指示。

NDIS 和过量驱动程序可以使用[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)OID 来设置或查询基础微型端口适配器的任务卸载封装设置。 [ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个[**ndis\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)结构。

 

 





