---
title: 中间驱动程序绑定操作
description: 中间驱动程序绑定操作
ms.assetid: 129a744c-d4d4-4741-9812-e76087c585fc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f7d9c30b1d75b611caf4f3e4e1f2686b3f76c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377887"
---
# <a name="intermediate-driver-binding-operations"></a>中间驱动程序绑定操作





当微型端口适配器可用时，会调用 NDIS [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数可以将绑定到该微型端口适配器任何中间驱动程序。

中间的驱动程序必须提供协议绑定操作中所述[绑定到适配器](binding-to-an-adapter.md)。

绑定时的操作包括分配并初始化绑定的特定于适配器的上下文区域、 初始化任何虚拟微型端口，将调用[ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)要绑定到适配器。

中间驱动程序不需要分配单独[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，每个绑定的池。 中间驱动程序所需分配 NET\_缓冲区\_列表结构池仅当驱动程序设计要求，以便分配其自己的结构。 否则，该驱动程序可以只需传递它接收来自其他驱动程序的结构。 此类驱动程序应将不同的池分配为发送和接收。

有关分配和管理网络数据的要求的信息，请参阅[中间驱动程序网络数据管理](intermediate-driver-network-data-management.md)。

 

 





