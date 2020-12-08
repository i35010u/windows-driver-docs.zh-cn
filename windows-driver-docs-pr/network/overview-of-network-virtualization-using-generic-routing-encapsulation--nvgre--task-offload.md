---
title: NVGRE 任务卸载概述
description: 介绍使用通用路由封装的网络虚拟化的概述 (NVGRE) 任务卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d1bd6331f1af2188801f5c4711ff8cbeddf04ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801333"
---
# <a name="overview-of-network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>有关使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化的概述


## <a name="nvgre-encapsulation-packet-format"></a>NVGRE 封装数据包格式

在这种情况下，协议或筛选器驱动程序将生成 (的非 LSO) 数据包，包括 GRE 封装，并将数据包发送到网络上。 在接收端，这些 (非 RSS，VMQ) 数据包将传递到协议驱动程序，无需任何修改。 请注意，NVGRE 任务卸载功能不指定封装和和解操作的卸载。

## <a name="send-and-receive-offloads"></a>发送和接收卸载

在发送路径上，以下任务卸载需要考虑到封装：

-   IPv4 和 TCP 或 UDP 有效负载的校验和计算
-   大量发送卸载版本 1 (LSO \_ v1) 和大量发送卸载版本 2 (LSO \_ v2) 

对于发送端卸载，小型端口必须在隧道上执行相应的操作 (外部) IP 标头、传输 (内部) IP 标头和 TCP 标头。

在接收路径上，以下任务卸载需要考虑到封装：

-   对 IPv4 和 TCP 或 UDP 有效负载的校验和验证
-   接收方缩放 (RSS) 
-   VMQ

对于接收端卸载，NIC 必须分析封装协议标头。 例如，对于 GRE 封装，NIC 必须分析 GRE 标头并在传输 (内部) 和/或隧道 (外部) IP 标头上执行任务卸载。

 

 





