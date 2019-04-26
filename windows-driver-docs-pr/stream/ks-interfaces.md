---
title: KS 接口
description: KS 接口
ms.assetid: cc6fad32-0587-44a8-92d1-54bc0370e5c0
keywords:
- 流式处理接口 WDK 内核
- KSPIN_INTERFACE
- 流式处理 WDK，接口的内核
- KS WDK 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfaa258619df88f0b8fbf11809b2ee5ddbe3258e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325235"
---
# <a name="ks-interfaces"></a>KS 接口





*接口*是定义 pin 的进行通信的描述符参数。 微型驱动程序指示 pin 支持通过提供指向的数组的指针的接口[ **KSPIN\_界面**](https://msdn.microsoft.com/library/windows/hardware/ff563537)中的相关结构[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)结构。 然后，KS 用于确定潜在的连接和关系图构建使用此信息。

媒体，如接口还介绍了作为一组以及该集的元素。 KSPIN\_接口结构定义的接口集内的特定接口。

用户模式下客户端然后通过使用指定的连接的接口的类型**接口**的相关成员[ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531)结构。 客户端传递此 KSPIN\_对的调用中的连接实例[ **KsCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff561652)，这会导致 IRP\_MJ\_创建发送到微型驱动程序。

 

 




