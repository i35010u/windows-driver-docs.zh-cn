---
title: 将安全关联添加到 NIC
description: 将安全关联添加到 NIC
keywords:
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
- 受 ESP 保护的数据包 WDK IPsec 卸载，安全关联
- 受 AH 保护的数据包 WDK IPsec 卸载，安全关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e746a4fc46f841131f523b9d5245a9df541ac6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822231"
---
# <a name="adding-a-security-association-to-a-nic"></a>将安全关联添加到 NIC

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 TCP/IP 传输确定某个 NIC 可以 (IPsec) 操作执行 Internet 协议安全时 (参阅 [报告 NIC 的 Ipsec 功能](reporting-a-nic-s-ipsec-capabilities.md)) ，该传输必须请求 nic 的微型端口驱动程序添加一个或多个 (SAs) 到 nic 的入站和出站安全关联，然后传输才能将 IPsec 任务卸载到 nic。 若要请求微型端口驱动程序将一个或多个 SAs 添加到 NIC，TCP/IP 传输会设置 [OID \_ TCP \_ 任务 " \_ IPSEC \_ 添加 \_ SA](./oid-tcp-task-ipsec-add-sa.md)"。

 

