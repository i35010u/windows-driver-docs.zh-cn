---
title: 处理 IRP
description: 处理 IRP
ms.assetid: 5fb6d2b9-17ee-4e76-95e9-dd5a7d1e79de
keywords:
- 内核模式驱动程序 WDK、Irp
- Irp WDK 内核
- I/o 请求数据包 WDK 内核，请参阅 Irp WDK 内核
- IRP WDK，请参阅 Irp WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4cec18327879127dd6c36aa7a83be510f9c9ac1
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402956"
---
# <a name="handling-irps"></a>处理 IRP





本部分介绍内核模式驱动程序如何处理 (Irp) 的 *i/o 请求包* 。 它包含以下部分：

[Windows I/O 模型概述](overview-of-the-windows-i-o-model.md)

[最终用户输入/输出请求和文件对象](end-user-i-o-requests-and-file-objects.md)

[I/O 请求的生命周期](example-i-o-request---an-overview.md)

[I/O 堆栈位置](i-o-stack-locations.md)

[I/O 状态块](i-o-status-blocks.md)

[向驱动程序堆栈的下层传递 IRP](passing-irps-down-the-driver-stack.md)

[为较低级驱动程序创建 IRP](creating-irps-for-lower-level-drivers.md)

[排队和取消排队 IRP](queuing-and-dequeuing-irps.md)

[完成 IRP](completing-irps.md)

[取消 IRP](canceling-irps.md)

[重复使用 IRP](reusing-irps.md)

[特定于设备类型的 I/O 请求](device-type-specific-i-o-requests.md)

[使用 I/O 控制代码](introduction-to-i-o-control-codes.md)

[使用 IRP 优先级提示](using-irp-priority-hints.md)

[IRP 主要函数代码](irp-major-function-codes.md)

[IRP 处理示例](processing-irps-in-a-lowest-level-driver.md)

 

 




