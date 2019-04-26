---
title: VMQ 发送和接收操作
description: VMQ 发送和接收操作
ms.assetid: 11f07534-f715-4ed5-b312-652fb3c7e8bb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c6eeb835b16950cac74047303ab54a6f2f47077
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327559"
---
# <a name="vmq-send-and-receive-operations"></a>VMQ 发送和接收操作





本部分提供有关实现发送信息和支持 VMQ 的 NDIS 驱动程序中接收操作。

若要支持 VMQ 发送和接收操作，VMQ 接口需要支持 VMQ 筛选器操作的网络适配器硬件。 这些筛选器确定数据包，以接收队列的分配。

本部分包括以下主题：

[VMQ 筛选器操作](vmq-filter-operations.md)

[共享的内存中接收缓冲区](shared-memory-in-receive-buffers.md)

[VMQ 接收路径](vmq-receive-path.md)

[VMQ 传输路径](vmq-transmit-path.md)

 

 





