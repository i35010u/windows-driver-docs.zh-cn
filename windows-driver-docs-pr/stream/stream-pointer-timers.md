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
ms.openlocfilehash: 262892eae0db30cfc978c44432bfbc054b1e5ab3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186263"
---
# <a name="stream-pointer-timers"></a>流指针计时器





若要在流指针上设置计时器，请调用 [**KsStreamPointerScheduleTimeout**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout)。 如果未在时间 *间隔内* 删除指定的流指针，则 AVStream 将调用供应商提供的计时器回调例程。 指定以100毫微秒为单位的 *间隔* 。

若要取消超时，请调用 [**KsStreamPointerCancelTimeout**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointercanceltimeout)。

 

