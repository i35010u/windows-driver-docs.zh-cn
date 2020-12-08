---
title: KS 接口
description: KS 接口
keywords:
- 接口 WDK 内核流式处理
- KSPIN_INTERFACE
- 内核流 WDK，接口
- KS WDK，接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 051fdcf3cb111cbacb6933e8c43a7090408090b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792513"
---
# <a name="ks-interfaces"></a>KS 接口





*接口* 是一个描述符参数，用于定义 pin 的通信方式。 微型驱动程序指示 pin 支持的接口，方法是在相关的 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中提供指向 [**KSPIN \_ 接口**](/previous-versions/ff563537(v=vs.85))结构数组的指针。 然后，KS 使用此信息来确定潜在连接和图形构建。

与媒体一样，接口也被描述为集的集合和元素。 KSPIN \_ 接口结构定义接口集内的特定接口。

然后，用户模式客户端使用相关 [**KSPIN \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)结构的 **interface** 成员指定连接的接口类型。 客户端 \_ 在对 [**KsCreatePin**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)的调用中传递此 KSPIN 连接实例，这将导致 IRP \_ MJ \_ 创建发送到微型驱动程序。

 

