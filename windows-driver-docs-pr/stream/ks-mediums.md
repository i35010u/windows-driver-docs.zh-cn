---
title: KS 媒体
description: KS 媒体
ms.assetid: c94c738c-66c6-491b-9157-28cccf95af4d
keywords:
- 媒体 WDK 内核流式处理
- KSPIN_MEDIUM
- 内核流 WDK，媒体
- KS WDK，介质
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d0b01dd4072c796bfe71d052c0edf37d9267dc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188183"
---
# <a name="ks-mediums"></a>KS 媒体





*中型*定义通信总线类型。 微型驱动程序通过提供指向相关[**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中[**KSPIN \_ MEDIUM**](/previous-versions/ff563538(v=vs.85))结构数组的指针来指示 pin 支持的媒体。 KSPIN \_ MEDIUM 标识通信总线上的特定连接。

客户端通过设置在对[**KsCreatePin**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)的调用中提供的[**KSPIN \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)结构中的**medium**成员，指定用于连接的介质。

客户端通过使用 [**KSPROPERTY \_ pin \_ 媒体**](./ksproperty-pin-mediums.md) 属性，请求筛选器或 pin 支持的媒体列表。

 

