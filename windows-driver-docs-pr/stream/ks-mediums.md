---
title: KS 媒体
description: KS 媒体
keywords:
- 媒体 WDK 内核流式处理
- KSPIN_MEDIUM
- 内核流 WDK，媒体
- KS WDK，介质
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f1a01cffed42cf7a3284130187dafc50f83647
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792511"
---
# <a name="ks-mediums"></a>KS 媒体





*中型* 定义通信总线类型。 微型驱动程序通过提供指向相关 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中 [**KSPIN \_ MEDIUM**](/previous-versions/ff563538(v=vs.85))结构数组的指针来指示 pin 支持的媒体。 KSPIN \_ MEDIUM 标识通信总线上的特定连接。

客户端通过设置在对 [**KsCreatePin**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)的调用中提供的 [**KSPIN \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)结构中的 **medium** 成员，指定用于连接的介质。

客户端通过使用 [**KSPROPERTY \_ pin \_ 媒体**](./ksproperty-pin-mediums.md) 属性，请求筛选器或 pin 支持的媒体列表。

 

