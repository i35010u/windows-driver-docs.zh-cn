---
title: 使用 TCP/IP 卸载管理员界面
description: 使用 TCP/IP 卸载管理员界面
keywords:
- TCP/IP 卸载 WDK 网络，管理员界面
- 卸载 WDK TCP/IP 传输，管理员界面
- 任务卸载 WDK TCP/IP 传输，管理员界面
- 连接卸载 WDK TCP/IP 传输，管理员界面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 356ecd0d0e9f18b6163674e9f2131babb63a9034
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248367"
---
# <a name="using-the-tcpip-offload-administrator-interface"></a>使用 TCP/IP 卸载管理员界面





在 NDIS 6.0 和更高版本中，用户模式应用程序 (或过量驱动程序) 可以启用或禁用 TCP/IP 卸载功能。 系统管理员可以通过 Microsoft Windows Management Instrumentation (WMI) 接口访问设置。 还可能会通过注册表设置禁用这些功能，如果硬件支持这些设置，则可以启用这些设置。

为了响应 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) 对象标识符 (oid) set 请求，微型端口驱动程序使用 [**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) 结构中的设置来设置微型端口适配器的当前卸载或连接卸载配置。

NDIS 在卸载标准化关键字的注册表中保留请求的设置。 当 NDIS 重新启动微型端口适配器时，微型端口驱动程序将读取卸载标准化关键字，并使用它们来设置 NIC 的默认卸载配置。 如果微型端口驱动程序还支持非标准关键字，则微型端口驱动程序会在更改任务卸载设置时负责更新注册表。 有关标准化关键字的详细信息，请参阅 [网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

微型端口驱动程序必须使用 [**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) 结构的内容来更新当前报告的卸载配置。 微型端口驱动程序必须报告当前配置，其中包含任务卸载 [**ndis \_ 状态任务 " \_ \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) " 或 "连接卸载 ndis \_ 状态 \_ 卸载 \_ 恢复状态指示"。  (有关 NDIS \_ 状态 \_ 卸载恢复的信息 \_ ，请参阅 [ndis 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。 ) 状态指示可确保所有的过量协议驱动程序都用新功能信息进行更新。

在用户模式应用程序 (或过量驱动程序) 设置 [OID \_ tcp \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) 之前，它们可以使用 [oid \_ tcp \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-offload-hardware-capabilities.md) oid 或 [oid \_ tcp \_ 连接 \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-connection-offload-hardware-capabilities.md) oid 来确定微型端口适配器的硬件可以支持哪些功能。 使用 OID \_ tcp \_ 卸载 \_ 参数 OID 来启用 [oid \_ tcp \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md) oid 或 [oid \_ tcp \_ 连接 \_ \_ \_ ](./oid-tcp-connection-offload-current-config.md) 的功能，以确保当前未启用当前配置 oid 报告。

例如，如果硬件功能改变 (例如，因为 MUX 中间驱动程序切换为差异基础微型端口适配器) ，所以，中间驱动程序必须使用 [**ndis \_ 状态 \_ 任务 " \_ 卸载 \_ 硬件 \_ 功能**](./ndis-status-task-offload-hardware-capabilities.md) " 或 " [**ndis \_ 状态 \_ TCP \_ 连接 \_ 卸载 \_ 硬件 \_ 功能**](./ndis-status-tcp-connection-offload-hardware-capabilities.md) " 状态指示来报告卸载硬件功能中的任何更改。

NDIS 和过量驱动程序可以使用 [OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) OID 来设置或查询基础微型端口适配器的任务卸载封装设置。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含 [**ndis \_ 卸载 \_ 封装**](/windows-hardware/drivers/ddi/encapsulationconfig/ns-encapsulationconfig-ndis_offload_encapsulation)结构。

 

