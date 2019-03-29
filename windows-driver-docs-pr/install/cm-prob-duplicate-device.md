---
title: CM_PROB_DUPLICATE_DEVICE
description: CM_PROB_DUPLICATE_DEVICE
ms.assetid: db0f6c98-d314-4882-ac8e-c73254f41c98
keywords:
- CM_PROB_DUPLICATE_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98cc72f297d125b5f55d64f6d02833a432cf7c32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567037"
---
# <a name="cmprobduplicatedevice"></a>CM_PROB_DUPLICATE_DEVICE

此函数保留供系统使用。

检测到重复的设备。

## <a name="error-code"></a>错误代码

42

### <a name="display-message"></a>显示消息

"Windows 无法加载这个硬件设备驱动程序是一个重复的设备已在系统中运行。 （代码 42）"

### <a name="recommended-resolution"></a>建议的解决方法

发生以下情况之一时，会报告此错误：

- 在操作系统注意到从旧位置缺少设备之前，在计算机中的新位置中发现具有序列号的设备。 这通常发生在设备移动时，可以非常快速地或当计算机处于待机状态或休眠状态，到其他位置。

    在这种情况下，您可以通过重新启动计算机来解决该问题。

- 总线驱动程序错误地在总线上创建两个具有相同名称的子级。 这被引起总线上报告相同的序列号的多个设备。 这也可能引起错误地报告相同的硬件标识符的两个或多个设备的总线驱动程序。

    在这种情况下，应联系[Microsoft 支持部门](http://support.microsoft.com/)获得更多帮助解决这个问题。
