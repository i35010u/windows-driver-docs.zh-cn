---
title: 在 AVStream 中处理互斥
description: 在 AVStream 中处理互斥
ms.assetid: dd84fe3f-352e-4641-99d7-792ccecb0b40
keywords:
- AVStream 互斥体 WDK
- 互斥体，WDK AVStream
- 处理互斥体 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1222e8ba8f8b43a139213f0aeb7acffcfdd810c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379061"
---
# <a name="processing-mutex-in-avstream"></a>在 AVStream 中处理互斥





第三个互斥体是处理互斥体。 单个筛选器和 pin 必须自己处理互斥体。 AVStream 独立获取处理在筛选器和 pin 级别之前, 处理互斥体以同步对处理相关结构的访问。 AVStream 也将获取处理 mutex 在其他操作，包括绑定到管道部分的插针，期间进入睡眠状态或唤醒电源操作，以及更改描述符。 微型驱动程序可以手动获取互斥体来执行同步操作，例如，处理或描述符修改。 它进行处理时不会发生任何更改之前，微型驱动程序应获取处理互斥体。

像其他两种类型的 mutex，处理互斥体，不获取以递归方式。 这意味着，如果微型驱动程序尝试获取在处理处理互斥体时，会发生死锁。

不要使用处理互斥体来暂停处理长一段时间。 而是直接通过使用操作处理控制门**KSGATE * Xxx*** 函数。

获取处理 mutex 的线程应随后尝试获取筛选器控件互斥体。

若要操作处理互斥体，使用以下函数：

[**KsFilterAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilteracquireprocessingmutex)， [ **KsPinAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinacquireprocessingmutex)， [ **KsFilterReleaseProcessingMutex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterreleaseprocessingmutex)， [ **KsPinReleaseProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinreleaseprocessingmutex)

 

 




