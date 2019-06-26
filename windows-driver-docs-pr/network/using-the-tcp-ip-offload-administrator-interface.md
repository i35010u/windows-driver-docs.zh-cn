---
title: 使用 TCP/IP 卸载管理员界面
description: 使用 TCP/IP 卸载管理员界面
ms.assetid: 2418e577-17cd-4db7-adb0-44b705e29d38
keywords:
- TCP/IP 卸载 WDK 网络管理员界面
- 卸载 WDK TCP/IP 传输，管理员界面
- 任务卸载，WDK TCP/IP 传输，管理员界面
- 连接将卸载 WDK TCP/IP 传输，管理员界面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8beb0feeed592dba04aff87441dc5ce56812f7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384372"
---
# <a name="using-the-tcpip-offload-administrator-interface"></a>使用 TCP/IP 卸载管理员界面





在 NDIS 6.0 和更高版本中，用户模式应用程序 （或基础驱动程序） 可以启用或禁用 TCP/IP 卸载功能。 系统管理员可以通过 Microsoft Windows Management Instrumentation (WMI) 界面访问这些设置。 此外可能通过注册表设置，当它们在硬件中受支持，才能启用禁用的功能。

以响应[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)对象标识符 (OID) 设置请求，微型端口驱动程序将使用中的设置[ **NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构微型端口适配器的当前卸载或连接卸载配置设置。

NDIS 会保留在卸载标准化关键字注册表中的请求的设置。 NDIS 重新启动时的微型端口适配器，微型端口驱动程序读取卸载标准化关键字，并使用它们来设置 NIC 的默认卸载配置 如果微型端口驱动程序还支持非标准关键字，微型端口驱动程序负责更新注册表更改的任务卸载设置时。 有关标准化关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

微型端口驱动程序必须使用的内容[ **NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构，以更新当前报告卸载配置。 微型端口驱动程序必须报告与该任务的当前配置将卸载[ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)或连接卸载 NDIS\_状态\_卸载\_恢复状态指示。 (有关信息 NDIS\_状态\_卸载\_恢复，请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。)状态指示可确保所有基础协议驱动程序使用新的功能信息更新。

用户模式应用程序 （或基础驱动程序） 设置前[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)可以使用[OID\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 或[OID\_TCP\_连接\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)OID若要确定微型端口适配器的硬件能够支持哪些功能。 使用 OID\_TCP\_卸载\_参数 OID 以启用功能的[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID 或[OID\_TCP\_连接\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)OID 报告为当前未启用。

如果硬件功能更改 （例如，因为 MUX 中间驱动程序将切换到不同基础微型端口适配器），中间驱动程序必须报告中与卸载的硬件功能的任何更改[ **NDIS\_状态\_任务\_卸载\_硬件\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)或[ **NDIS\_状态\_TCP\_连接\_卸载\_硬件\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-tcp-connection-offload-hardware-capabilities)状态指示。

NDIS 和基础驱动程序可以使用[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)OID 设置或查询任务卸载的基础的微型端口适配器封装设置。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含[ **NDIS\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)结构。

 

 





