---
title: 将安全关联添加到 NIC
description: 将安全关联添加到 NIC
ms.assetid: 524cc9f8-fe02-4192-85af-83813ae83d08
keywords:
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
- 受 ESP 保护的数据包 WDK IPsec 卸载，安全关联
- 受 AH 保护的数据包 WDK IPsec 卸载，安全关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 968888bfd30f3a67dc86d99c29f0545c3f548209
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218177"
---
# <a name="adding-a-security-association-to-a-nic"></a>将安全关联添加到 NIC

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 TCP/IP 传输确定某个 NIC 可以 (IPsec) 操作执行 Internet 协议安全时 (参阅 [报告 NIC 的 Ipsec 功能](reporting-a-nic-s-ipsec-capabilities.md)) ，该传输必须请求 nic 的微型端口驱动程序添加一个或多个 (SAs) 到 nic 的入站和出站安全关联，然后传输才能将 IPsec 任务卸载到 nic。 若要请求微型端口驱动程序将一个或多个 SAs 添加到 NIC，TCP/IP 传输会设置 [OID \_ TCP \_ 任务 " \_ IPSEC \_ 添加 \_ SA](./oid-tcp-task-ipsec-add-sa.md)"。

 

