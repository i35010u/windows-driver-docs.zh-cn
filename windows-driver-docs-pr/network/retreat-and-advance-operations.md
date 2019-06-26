---
title: 重新处理和前进操作
description: 重新处理和前进操作
ms.assetid: 90d4acae-e66c-486b-8b38-59f7fe159047
keywords:
- 网络数据 WDK，提前操作
- 网络 WDK，参加操作数据
- 数据 WDK 网络，提前操作
- 数据 WDK 网络，参加操作
- 数据包 WDK 网络，提前操作
- 数据包 WDK 网络，参加操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03bc41e1ba5bc8af3061492005ab700b23ce06e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373885"
---
# <a name="retreat-and-advance-operations"></a>重新处理和前进操作





NDIS 提供参加和高级函数可操纵[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。 [参加 operations](retreat-operations.md)进行更多*用数据空间*供当前驱动程序。 [继续学习 operations](advance-operations.md)释放*用数据空间*。

在发送操作期间，参加操作都是必需或当驱动程序返回接收到对基础驱动程序的数据。 例如，在发送操作中，驱动程序可以调用[ **NdisRetreatNetBufferDataStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisretreatnetbufferdatastart)函数的标头数据留出空间。

发送操作何时完成，或当驱动程序从基础驱动程序收到数据时所需的高级操作数。 例如，在接收操作中，驱动程序可以调用[ **NdisAdvanceNetBufferDataStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisadvancenetbufferdatastart)函数将跳过已由较低级别的驱动程序的标头数据。 在这种情况下，标头数据保持的缓冲区*未使用的数据空间*。

下图显示了网络数据和这些操作之间的关系。

![说明数据空间分配的关系图](images/netbufferdata-basic.png)

以下主题提供有关高级和撤回操作的详细信息：

[参加操作](retreat-operations.md)

[高级操作](advance-operations.md)

 

 





