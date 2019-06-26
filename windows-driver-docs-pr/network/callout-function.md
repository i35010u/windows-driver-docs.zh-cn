---
title: 标注函数
description: 标注函数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- 标注函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a64682863c16ba3aa111bf1710e1c1b5b6d98245
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382810"
---
# <a name="callout-function"></a>标注函数


一个*标注函数*是一个函数，由实现[标注驱动程序](callout-driver.md)，它是定义的函数之一[标注](callout.md)。 下面的标注函数列表包含一个标注：

-   一个[ *notifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)函数来处理通知。

-   一个[ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)进程分类的函数。

-   一个[ *flowDeleteFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)过程流删除操作 （可选） 的函数。

[筛选器引擎](filter-engine.md)标注的标注函数以便标注可以处理的网络数据的调用。

 

 





