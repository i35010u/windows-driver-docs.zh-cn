---
title: Hyper-v 可扩展交换机转发上下文概述
description: Hyper-v 可扩展交换机转发上下文概述
ms.assetid: B2BF07B5-FA44-4994-9605-EFF4A0B9179F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb734efaf5db91ba8f32f94767bb5e2a547b0d1b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565675"
---
# <a name="hyper-v-extensible-switch-forwarding-context-overview"></a>Hyper-v 可扩展交换机转发上下文概述


遍历 hyper-v 可扩展交换机数据路径的每个数据包的[ **\_网络缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构包含带外 (OOB) 数据。 此数据指定从其发起数据包的源端口, 以及用于数据包传递的一个或多个目标端口。 此 OOB 数据称为*可扩展交换机转发上下文*。

本部分包括有关可扩展交换机转发上下文的下列主题:

[Hyper-v 可扩展交换机转发上下文数据类型](hyper-v-extensible-switch-forwarding-context-data-types.md)

[管理 Hyper-v 可扩展交换机转发上下文](managing-the-hyper-v-extensible-switch-forwarding-context.md)

 

 





