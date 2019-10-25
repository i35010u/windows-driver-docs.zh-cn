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
ms.openlocfilehash: 7c3e6dd6a4c8a1dec4de235b6980986595035fce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842515"
---
# <a name="ks-mediums"></a>KS 媒体





*中型*定义通信总线类型。 微型驱动程序通过在相关[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构中提供一个指向[**KSPIN\_MEDIUM**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))结构的数组的指针来指示 pin 支持的媒体。 KSPIN\_MEDIUM 标识通信总线上的特定连接。

客户端通过设置在对[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)的调用中提供的[**KSPIN\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)结构中的**medium**成员，指定用于连接的介质。

客户端通过使用[**KSPROPERTY\_pin\_媒体**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-mediums)属性，请求筛选器或 pin 支持的媒体列表。

 

 




