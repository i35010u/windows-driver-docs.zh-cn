---
title: 流指针计时器
description: 流指针计时器
keywords:
- 流指针 WDK AVStream，计时器
- 计时器 WDK AVStream
- 超时 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39b197c58fac5d4a243b90a5bd9aa475a485d97e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839845"
---
# <a name="stream-pointer-timers"></a>流指针计时器





若要在流指针上设置计时器，请调用 [**KsStreamPointerScheduleTimeout**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout)。 如果未在时间 *间隔内* 删除指定的流指针，则 AVStream 将调用供应商提供的计时器回调例程。 指定以100毫微秒为单位的 *间隔* 。

若要取消超时，请调用 [**KsStreamPointerCancelTimeout**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointercanceltimeout)。

 

