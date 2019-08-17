---
title: 适用于卸载的微型端口驱动程序的安全指南概述
description: 适用于卸载的微型端口驱动程序的安全指南概述
ms.assetid: 178be416-3936-4e17-b055-134897b3e2eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b88c1cfd7cedcacab1a9e7888fa6f8e96fd51e8
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565641"
---
# <a name="security-guidelines-for-offload-capable-miniport-drivers-overview"></a>适用于卸载的微型端口驱动程序的安全指南概述

为了提高性能, Microsoft TCP/IP 传输可将任务或连接卸载到具有适当 TCP/IP 卸载功能的网络接口卡 (NIC)。 卸载的 TCP/IP 网络通信任务在 NIC 硬件中进行处理。 微型端口驱动程序将 NIC 硬件的各种卸载功能播发到操作系统, 并 confugure NIC 硬件。 NIC 硬件在发送和接收调度处理程序中对传出和传入数据包执行播发的卸载任务。 硬件执行计算 IP 标头校验和等操作。

若要确保安全环境, 小型端口驱动程序应仅公布 NIC 硬件可以提供的卸载功能, 而不是其他设备。 微型端口驱动程序应将硬件配置为卸载满足播发条件的数据包上的播发任务。 在发送路径上, 操作系统不需要驱动程序来卸载微型端口驱动程序未播发的任务。 在接收路径上, 微型端口驱动程序和 NIC 不应执行任何不包含在微型端口驱动程序公布的 NIC 硬件功能中的任务。

如果微型端口驱动程序或 NIC 无法在收到的数据包上执行卸载任务, 微型端口驱动程序应在无需执行任何操作的情况下将此类数据包放置在驱动程序堆栈上。 在这种情况下, 过量驱动程序会将数据包作为常规数据包处理。

微型端口驱动程序绝不应公布 NIC 硬件不支持的功能。 微型端口驱动程序绝不应使用发送或接收调度处理程序来执行硬件无法提供的卸载操作的软件模拟。 如果微型端口驱动程序提供了此类软件仿真, 则驱动程序必须检查软件中的数据包数据。 如果驱动程序检查软件中的数据包数据, 则计算机可能会受到安全攻击。

以下主题提供了有关安全攻击的详细信息, 以及如何避免 NDIS 驱动程序中的安全问题:

[NDIS 驱动程序中安全攻击的漏洞](vulnerability-to-security-attacks-in-ndis-drivers.md)

[NDIS 驱动程序中的性能下降和拒绝服务攻击](performance-degradation-and-denial-of-service-attacks-in-ndis-drivers.md)

[增加了测试易受攻击的 NDIS 驱动程序的成本](added-costs-for-testing-vulnerable-ndis-drivers.md)

[NDIS 驱动程序的安全清单](security-checklist-for-ndis-drivers.md)