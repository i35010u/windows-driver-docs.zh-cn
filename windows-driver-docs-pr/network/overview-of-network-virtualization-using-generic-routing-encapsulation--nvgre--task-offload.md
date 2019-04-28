---
title: NVGRE 任务卸载的概述
description: 介绍使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化概述
ms.assetid: 5890AF7E-93E1-4E19-B483-C75657D749EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3482ebacd55cc5044f568a945548cf1eaca966a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343227"
---
# <a name="overview-of-network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>有关使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化的概述


## <a name="nvgre-encapsulation-packet-format"></a>NVGRE 封装数据包格式

在这种情况下，协议或筛选器驱动程序将生成的 (非 LSO) 数据包，包括 GRE 封装，并在网络上发送数据包。 在接收端，这些 (非-RSS，VMQ) 数据包传递给不进行任何修改协议驱动程序。 请注意 NVGRE 任务卸载功能未指定封装和解封操作的卸载。

## <a name="send-and-receive-offloads"></a>发送和接收卸载

发送路径上的以下任务卸载需要封装到帐户：

-   IPv4 和 TCP 或 UDP 负载的校验和计算
-   大量发送卸载版本 1 (LSO\_v1) 和大量发送卸载版本 2 (LSO\_v2)

对发送端卸载，微型端口必须执行相应操作隧道 （外部） IP 标头、 传输 （内部联接） IP 标头和 TCP 标头。

接收路径上的以下任务卸载需要封装到帐户：

-   IPv4 和 TCP 或 UDP 负载的校验和验证
-   接收方缩放 (RSS)
-   VMQ

为接收方卸载 NIC 必须分析封装协议标头。 例如，对于 GRE 封装 NIC 必须分析 GRE 报头并执行任务卸载 （内部） 传输和/或隧道 （外部） IP 标头。

 

 





