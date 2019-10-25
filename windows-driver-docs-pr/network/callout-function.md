---
title: 标注函数
description: 标注函数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- 标注函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d440d233c9988d05e8d7fdebc04afcb3d205fac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838210"
---
# <a name="callout-function"></a>标注函数


*标注函数*是由[标注驱动程序](callout-driver.md)实现的一个函数，该驱动程序是定义[标注](callout.md)的函数之一。 标注由以下标注函数列表组成：

-   用于处理通知的[*notifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)函数。

-   用于处理分类的[*classifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)函数。

-   用于处理流删除的[*flowDeleteFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)函数（可选）。

[筛选器引擎](filter-engine.md)将调用标注的标注函数，以便标注能够处理网络数据。

 

 





