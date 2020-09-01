---
title: Hyper-V 可扩展交换机转发上下文概述
description: Hyper-V 可扩展交换机转发上下文概述
ms.assetid: B2BF07B5-FA44-4994-9605-EFF4A0B9179F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06802524c4ac0253e620d877e0b7db8237d2005d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214728"
---
# <a name="hyper-v-extensible-switch-forwarding-context-overview"></a>Hyper-V 可扩展交换机转发上下文概述


遍历 Hyper-v 可扩展交换机数据路径的每个数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构包含带外 (OOB) 数据。 此数据指定从其发起数据包的源端口，以及用于数据包传递的一个或多个目标端口。 此 OOB 数据称为 *可扩展交换机转发上下文*。

本部分包括有关可扩展交换机转发上下文的下列主题：

[Hyper-V 可扩展交换机转发上下文数据类型](hyper-v-extensible-switch-forwarding-context-data-types.md)

[管理 Hyper-V 可扩展交换机转发上下文](managing-the-hyper-v-extensible-switch-forwarding-context.md)

 

