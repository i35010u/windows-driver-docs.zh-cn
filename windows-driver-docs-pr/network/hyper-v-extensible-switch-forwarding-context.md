---
title: Hyper-V 可扩展交换机转发上下文概述
description: Hyper-V 可扩展交换机转发上下文概述
ms.assetid: B2BF07B5-FA44-4994-9605-EFF4A0B9179F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9c817ef13e498bee0a781f49c1a3ff62b0d3559
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823891"
---
# <a name="hyper-v-extensible-switch-forwarding-context-overview"></a>Hyper-V 可扩展交换机转发上下文概述


遍历 Hyper-v 可扩展交换机数据路径的每个数据包的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构包含带外（OOB）数据。 此数据指定从其发起数据包的源端口，以及用于数据包传递的一个或多个目标端口。 此 OOB 数据称为*可扩展交换机转发上下文*。

本部分包括有关可扩展交换机转发上下文的下列主题：

[Hyper-v 可扩展交换机转发上下文数据类型](hyper-v-extensible-switch-forwarding-context-data-types.md)

[管理 Hyper-v 可扩展交换机转发上下文](managing-the-hyper-v-extensible-switch-forwarding-context.md)

 

 





