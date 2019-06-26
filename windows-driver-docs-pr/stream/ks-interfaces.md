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
ms.openlocfilehash: 574853d4d05fb0fff7a384e4a14b60846833fe5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382498"
---
# <a name="ks-interfaces"></a>KS 接口





*接口*是定义 pin 的进行通信的描述符参数。 微型驱动程序指示 pin 支持通过提供指向的数组的指针的接口[ **KSPIN\_界面**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))中的相关结构[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)结构。 然后，KS 用于确定潜在的连接和关系图构建使用此信息。

媒体，如接口还介绍了作为一组以及该集的元素。 KSPIN\_接口结构定义的接口集内的特定接口。

用户模式下客户端然后通过使用指定的连接的接口的类型**接口**的相关成员[ **KSPIN\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_connect)结构。 客户端传递此 KSPIN\_对的调用中的连接实例[ **KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)，这会导致 IRP\_MJ\_创建发送到微型驱动程序。

 

 




