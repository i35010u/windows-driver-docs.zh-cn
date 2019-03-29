---
title: 支持卸载的微型端口驱动程序安全指导原则
description: 支持卸载的微型端口驱动程序安全指导原则
ms.assetid: 178be416-3936-4e17-b055-134897b3e2eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a08a704e0ec1db82a5208f4f2b2160165ad1f84b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566649"
---
# <a name="security-guidelines-for-offload-capable-miniport-drivers"></a>支持卸载的微型端口驱动程序安全指导原则





若要提高其性能，可以将任务或连接到网络接口卡 (NIC) 具有相应的 TCP/IP-卸载功能会卸载 Microsoft TCP/IP 传输。 卸载的 TCP/IP 网络通信任务处理在 NIC 硬件中。 微型端口驱动程序播发到的操作系统和 confugure NIC 硬件 NIC 硬件的各种卸载功能。 NIC 硬件播发的卸载任务对传出和传入数据包中发送和接收调度处理程序。 硬件执行操作，如计算 IP 标头校验和，依此类推。

若要确保安全的环境，微型端口驱动程序应将播发仅卸载 NIC 硬件可以提供的功能，但不其他人。 微型端口驱动程序应配置硬件卸载上满足播发的条件的数据包播发的任务。 发送路径上的操作系统不需要的驱动程序来卸载微型端口驱动程序未不播发的任务。 接收路径上的微型端口驱动程序和 NIC 不应执行中的微型端口驱动程序播发的 NIC 硬件功能不包含任何任务。

如果微型端口驱动程序或 NIC 无法执行卸载任务上接收的数据包，微型端口驱动程序应指示驱动程序堆栈上的此类数据包，而无需采取任何操作。 在这种情况下，基础驱动程序作为普通数据包处理数据包。

微型端口驱动程序应永远不会播发 NIC 硬件不支持的功能。 微型端口驱动程序应永远不会使用发送或接收调度处理程序来执行软件模拟的硬件不能提供的卸载操作。 如果微型端口驱动程序提供了此类软件模拟，该驱动程序必须检查软件中的数据包数据。 如果该驱动程序将检查软件中的数据包数据，计算机可能会面临安全攻击。

以下主题提供有关安全攻击的详细信息以及如何避免的 NDIS 驱动程序中的安全问题：

[在 NDIS 驱动程序中的安全漏洞攻击](vulnerability-to-security-attacks-in-ndis-drivers.md)

[性能下降，拒绝服务攻击的 NDIS 驱动程序中](performance-degradation-and-denial-of-service-attacks-in-ndis-drivers.md)

[用于测试的易受攻击的 NDIS 驱动程序添加了的成本](added-costs-for-testing-vulnerable-ndis-drivers.md)

[NDIS 驱动程序的安全清单](security-checklist-for-ndis-drivers.md)

 

 





