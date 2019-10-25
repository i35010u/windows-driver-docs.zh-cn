---
title: KS 接口
description: KS 接口
ms.assetid: cc6fad32-0587-44a8-92d1-54bc0370e5c0
keywords:
- 接口 WDK 内核流式处理
- KSPIN_INTERFACE
- 内核流 WDK，接口
- KS WDK，接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 575992aec5b1e33801aa4395c0d7c6dcc866aff3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844350"
---
# <a name="ks-interfaces"></a>KS 接口





*接口*是一个描述符参数，用于定义 pin 的通信方式。 微型驱动程序通过在相关[**KSPIN\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中提供指向[**KSPIN\_接口**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))结构的数组的指针来指示 pin 支持的接口。 然后，KS 使用此信息来确定潜在连接和图形构建。

与媒体一样，接口也被描述为集的集合和元素。 KSPIN\_接口结构定义接口集内的特定接口。

然后，用户模式客户端使用相关[ **\_KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)的**接口**成员指定连接的接口类型。 在对[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)的调用中，客户端传递此 KSPIN\_连接实例，这将导致 IRP\_MJ\_创建发送到微型驱动程序。

 

 




