---
title: 重新处理和前进操作
description: 重新处理和前进操作
keywords:
- 网络数据 WDK，高级操作
- 网络数据 WDK，撤回操作
- 数据 WDK 网络，高级操作
- 数据 WDK 网络，撤回操作
- 包 WDK 网络，高级操作
- 包 WDK 网络，撤回操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee1a658720412532a4cdb4f3887b0435b4cfe830
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813633"
---
# <a name="retreat-and-advance-operations"></a>重新处理和前进操作





NDIS 提供了用于操作 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构的撤回和高级功能。 [撤回操作](retreat-operations.md) 使当前驱动程序可以使用更多的可用 *数据空间* 。 [高级操作](advance-operations.md) 版本 *使用的数据空间*。

在发送操作期间或者当驱动程序将接收的数据返回到基础驱动程序时，需要执行撤回操作。 例如，在发送操作期间，驱动程序可以调用 [**NdisRetreatNetBufferDataStart**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart) 函数来为标头数据腾出空间。

当发送操作完成或驱动程序从基础驱动程序接收数据时，需要高级操作。 例如，在接收操作期间，驱动程序可以调用 [**NdisAdvanceNetBufferDataStart**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart) 函数来跳过较低级别驱动程序使用的标头数据。 在这种情况下，标头数据将保留在缓冲区中 *未使用的数据空间* 内。

下图显示了网络数据和这些操作之间的关系。

![说明数据空间分配的关系图](images/netbufferdata-basic.png)

以下主题提供了有关高级和撤回操作的详细信息：

[重新处理操作](retreat-operations.md)

[前进操作](advance-operations.md)

 

