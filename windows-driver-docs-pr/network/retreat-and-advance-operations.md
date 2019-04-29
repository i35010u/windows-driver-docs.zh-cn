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
ms.openlocfilehash: ed28a175b80fa6a74e019968d00fffad49bba9c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391648"
---
# <a name="retreat-and-advance-operations"></a>重新处理和前进操作





NDIS 提供参加和高级函数可操纵[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 [参加 operations](retreat-operations.md)进行更多*用数据空间*供当前驱动程序。 [继续学习 operations](advance-operations.md)释放*用数据空间*。

在发送操作期间，参加操作都是必需或当驱动程序返回接收到对基础驱动程序的数据。 例如，在发送操作中，驱动程序可以调用[ **NdisRetreatNetBufferDataStart** ](https://msdn.microsoft.com/library/windows/hardware/ff564527)函数的标头数据留出空间。

发送操作何时完成，或当驱动程序从基础驱动程序收到数据时所需的高级操作数。 例如，在接收操作中，驱动程序可以调用[ **NdisAdvanceNetBufferDataStart** ](https://msdn.microsoft.com/library/windows/hardware/ff560703)函数将跳过已由较低级别的驱动程序的标头数据。 在这种情况下，标头数据保持的缓冲区*未使用的数据空间*。

下图显示了网络数据和这些操作之间的关系。

![说明数据空间分配的关系图](images/netbufferdata-basic.png)

以下主题提供有关高级和撤回操作的详细信息：

[参加操作](retreat-operations.md)

[高级操作](advance-operations.md)

 

 





