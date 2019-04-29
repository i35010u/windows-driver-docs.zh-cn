---
title: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
description: CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.assetid: c7639fd7-738f-4115-9abc-0bafca097b9e
keywords:
- CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4797c3c15795b203221bd0176652721ee1c91e16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358993"
---
# <a name="cmprobdriverfailedpriorunload"></a>CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD

此函数保留供系统使用。

无法加载该驱动程序，因为前一个实例仍处于加载状态。

## <a name="error-code"></a>错误代码

38

### <a name="display-message"></a>显示消息

"Windows 由于无法加载这个硬件设备驱动程序的设备驱动程序的前一个实例仍在内存中。 （代码 38）"

### <a name="recommended-resolution"></a>建议的解决方法

以前的驱动程序实例仍可以因不正确的引用计数或之间负载争用而加载和卸载操作。 此外，会出现此消息，如果驱动程序引用由多个[ **INF AddService 指令**](inf-addservice-directive.md)中一个或多个 INF 文件。

选择**重新启动计算机**，这将重新启动计算机。
