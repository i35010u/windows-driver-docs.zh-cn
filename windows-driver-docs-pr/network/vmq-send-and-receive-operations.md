---
title: VMQ 发送和接收操作
description: VMQ 发送和接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fcd61dabd1663026829300b5a09a8e1171f4119
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786703"
---
# <a name="vmq-send-and-receive-operations"></a>VMQ 发送和接收操作





本部分提供有关在支持 VMQ 的 NDIS 驱动程序中实现发送和接收操作的信息。

为了支持 VMQ 发送和接收操作，VMQ 接口需要支持 VMQ 筛选器操作的网络适配器硬件。 这些筛选器确定用于接收队列的数据包的分配。

本节包括下列主题：

[VMQ 筛选器操作](vmq-filter-operations.md)

[接收缓冲区中的共享内存](shared-memory-in-receive-buffers.md)

[VMQ 接收路径](vmq-receive-path.md)

[VMQ 传输路径](vmq-transmit-path.md)

 

 





