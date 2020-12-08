---
title: 任务卸载 OID
description: 本主题介绍任务卸载 Oid
keywords:
- 任务卸载 Oid，任务卸载 NDIS Oid，任务卸载 Oid WDK，任务卸载 Oid 网络
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: b13c109fef8f8f397bd67d25dc470722559bb076
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803489"
---
# <a name="task-offload-oids"></a>任务卸载 OID

下表汇总了支持 TCP/IP 任务卸载操作的 Oid。 有关此类操作的详细信息，请参阅 [Tcp/ip 任务卸载](task-offload.md)。-ndis-status-dot11-wfd-group-operating-channel.md

在此表中，M 指示 OID 是必需的，而 O 指示它是可选的。

| 长度 | 查询 | 设置 | “属性” |
| --- | --- | --- | --- |
| Arr |   | M | [OID_TCP_TASK_IPSEC_ADD_SA](oid-tcp-task-ipsec-add-sa.md) |
| Arr |   | M | [OID_TCP_TASK_IPSEC_ADD_UDPESP_SA](oid-tcp-task-ipsec-add-udpesp-sa.md) |
| 4 |   | M | [OID_TCP_TASK_IPSEC_DELETE_SA](oid-tcp-task-ipsec-delete-sa.md) |
| 4 |   | M | [OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA](oid-tcp-task-ipsec-delete-udpesp-sa.md) |
| Arr | M | M | [OID_TCP_TASK_OFFLOAD](oid-tcp-task-offload.md) |

