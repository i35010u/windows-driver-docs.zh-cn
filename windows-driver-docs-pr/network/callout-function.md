---
title: 标注函数
description: 标注函数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- 标注函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eadb245ece6e3bb7c75937f83abebae6ee5a326d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212539"
---
# <a name="callout-function"></a>标注函数


*标注函数*是由[标注驱动程序](callout-driver.md)实现的一个函数，该驱动程序是定义[标注](callout.md)的函数之一。 标注由以下标注函数列表组成：

-   用于处理通知的 [*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) 函数。

-   用于处理分类的 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 函数。

-   用于处理流删除 (可选) 的 [*flowDeleteFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0) 函数。

[筛选器引擎](filter-engine.md)将调用标注的标注函数，以便标注能够处理网络数据。

 

