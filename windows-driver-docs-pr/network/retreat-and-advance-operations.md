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
ms.openlocfilehash: c1d727bde41fcb24116f18aaa06789cbde87dde4
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248980"
---
# <a name="retreat-and-advance-operations"></a>重新处理和前进操作





NDIS 提供了用于操作 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构的撤回和高级功能。 [撤回操作](retreat-operations.md) 使当前驱动程序可以使用更多的可用 *数据空间* 。 [高级操作](advance-operations.md) 版本 *使用的数据空间*。

在发送操作期间或者当驱动程序将接收的数据返回到基础驱动程序时，需要执行撤回操作。 例如，在发送操作期间，驱动程序可以调用 [**NdisRetreatNetBufferDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisretreatnetbufferdatastart) 函数来为标头数据腾出空间。

当发送操作完成或驱动程序从基础驱动程序接收数据时，需要高级操作。 例如，在接收操作期间，驱动程序可以调用 [**NdisAdvanceNetBufferDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisadvancenetbufferdatastart) 函数来跳过较低级别驱动程序使用的标头数据。 在这种情况下，标头数据将保留在缓冲区中 *未使用的数据空间* 内。

下图显示了网络数据和这些操作之间的关系。

![说明数据空间分配的关系图](images/netbufferdata-basic.png)

以下主题提供了有关高级和撤回操作的详细信息：

[重新处理操作](retreat-operations.md)

[前进操作](advance-operations.md)

 

