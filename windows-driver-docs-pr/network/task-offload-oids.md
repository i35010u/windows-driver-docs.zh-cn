---
title: 任务卸载 OID
description: 本主题介绍了任务卸载 Oid
ms.assetid: 0d7eab31-d5c9-4264-9598-c72e19e1d86b
keywords:
- 任务卸载 Oid、 任务卸载 NDIS Oid、 任务卸载 Oid WDK、 任务卸载的网络的 Oid
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53088e50e0d771d1bf79add695b07547e5c5a5fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368219"
---
# <a name="task-offload-oids"></a>任务卸载 OID

下表汇总了支持 TCP/IP 任务卸载操作的 Oid。 有关此类操作的详细信息，请参阅[TCP/IP 任务卸载](task-offload.md).-ndis-status-dot11-wfd-group-operating-channel.md

在此表中，M 指示 OID 是必需的而 O 则指示它是可选的。

| 长度 | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| arr |   | M | [OID_TCP_TASK_IPSEC_ADD_SA](oid-tcp-task-ipsec-add-sa.md) |
| arr |   | M | [OID_TCP_TASK_IPSEC_ADD_UDPESP_SA](oid-tcp-task-ipsec-add-udpesp-sa.md) |
| 4 |   | M | [OID_TCP_TASK_IPSEC_DELETE_SA](oid-tcp-task-ipsec-delete-sa.md) |
| 4 |   | M | [OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA](oid-tcp-task-ipsec-delete-udpesp-sa.md) |
| arr | M | M | [OID_TCP_TASK_OFFLOAD](oid-tcp-task-offload.md) |

