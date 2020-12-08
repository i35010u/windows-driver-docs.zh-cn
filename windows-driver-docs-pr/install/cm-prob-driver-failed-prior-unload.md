---
title: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
description: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
keywords:
- CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcea6e0db42889096e29d2e1691f160c5a32a563
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783171"
---
# <a name="code-38---cm_prob_driver_failed_prior_unload"></a>代码 38 - CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD

此设备管理器错误消息指示由于仍在加载上一个实例，因此无法加载驱动程序。

## <a name="error-code"></a>错误代码

38

### <a name="display-message"></a>显示消息

"Windows 无法加载此硬件的设备驱动程序，因为设备驱动程序的前一个实例仍在内存中。  (代码 38) "

### <a name="recommended-resolution"></a>推荐的解决方案

由于不正确的引用计数或负载操作与卸载操作之间存在争用，因此仍可加载以前的驱动程序实例。 此外，如果一个或多个 inf 文件中有多个 [**Inf AddService 指令**](inf-addservice-directive.md) 引用了驱动程序，则会出现此消息。

选择 " **重新启动计算机**"，这将重新启动计算机。
