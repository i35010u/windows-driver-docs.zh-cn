---
title: 流指针计时器
description: 流指针计时器
ms.assetid: 98413fc6-2b62-4c52-9ac4-bd2a3a60db60
keywords:
- 流指针 WDK AVStream，计时器
- 计时器 WDK AVStream
- 超时 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10317e951a5f6e606d46194554eb2343aa674e55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377801"
---
# <a name="stream-pointer-timers"></a>流指针计时器





若要在流指针上设置一个计时器，调用[ **KsStreamPointerScheduleTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerscheduletimeout)。 如果按时间未被删除了指定的流指针*间隔*过期，AVStream 调用供应商提供的计时器回调例程。 指定*间隔*以 100 毫微秒为单位。

若要取消超时，请调用[ **KsStreamPointerCancelTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointercanceltimeout)。

 

 




