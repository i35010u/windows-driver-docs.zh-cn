---
title: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
description: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.assetid: c7639fd7-738f-4115-9abc-0bafca097b9e
keywords:
- CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d03c0461ce5abeb9c8e2cdbb33226562d3b071
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279580"
---
# <a name="code-38---cm_prob_driver_failed_prior_unload"></a>代码 38-CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD

此设备管理器错误消息指示由于仍在加载上一个实例，因此无法加载驱动程序。

## <a name="error-code"></a>错误代码

38

### <a name="display-message"></a>显示消息

"Windows 无法加载此硬件的设备驱动程序，因为设备驱动程序的前一个实例仍在内存中。 （代码38） "

### <a name="recommended-resolution"></a>建议的解决方法

由于不正确的引用计数或负载操作与卸载操作之间存在争用，因此仍可加载以前的驱动程序实例。 此外，如果一个或多个 inf 文件中有多个[**Inf AddService 指令**](inf-addservice-directive.md)引用了驱动程序，则会出现此消息。

选择 "**重新启动计算机**"，这将重新启动计算机。
