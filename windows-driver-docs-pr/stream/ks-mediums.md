---
title: KS 媒体
description: KS 媒体
ms.assetid: c94c738c-66c6-491b-9157-28cccf95af4d
keywords:
- 流式处理媒体 WDK 内核
- KSPIN_MEDIUM
- WDK、 媒体流式处理的内核
- KS WDK 介质
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 291aa5d20d1bd04ae26191f304517ce6d9c4bcf9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382504"
---
# <a name="ks-mediums"></a>KS 媒体





一个*中等*定义一种类型的通信总线。 微型驱动程序指示 pin 支持通过提供指向的数组的指针的媒介[ **KSPIN\_MEDIUM** ](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))中的相关结构[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)结构。 KSPIN\_中等标识通信总线上的特定连接。

客户端指定要通过设置用于连接的介质**中等**中的成员[ **KSPIN\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_connect)它们对的调用中提供的结构[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)。

客户端请求一系列媒体通过使用支持的筛选器或 pin [ **KSPROPERTY\_PIN\_媒介**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-mediums)属性。

 

 




