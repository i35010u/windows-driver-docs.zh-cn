---
title: 处理 Irp
description: 处理 Irp
ms.assetid: 5fb6d2b9-17ee-4e76-95e9-dd5a7d1e79de
keywords:
- 内核模式驱动程序 WDK Irp
- Irp WDK 内核
- I/O 请求数据包 WDK 内核请参阅 Irp WDK 内核
- IRP WDK，请参阅 Irp WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30221c07b1887e56123e285e6f5017e23548e8af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521171"
---
# <a name="handling-irps"></a>处理 Irp





本部分介绍内核模式驱动程序如何处理*I/O 请求数据包*(Irp)。 它包含以下各节：

[Windows I/O 模型概述](overview-of-the-windows-i-o-model.md)

[最终用户输入/输出请求和文件对象](end-user-i-o-requests-and-file-objects.md)

[I/O 请求的生命周期](the-life-of-an-i-o-request.md)

[I/O 堆栈位置](i-o-stack-locations.md)

[I/O 状态数据块](i-o-status-blocks.md)

[将驱动程序堆栈的下层的 Irp 传递](passing-irps-down-the-driver-stack.md)

[创建 Irp 的较低级驱动程序](creating-irps-for-lower-level-drivers.md)

[排队和取消排队 Irp](queuing-and-dequeuing-irps.md)

[完成 Irp](completing-irps.md)

[正在取消 Irp](canceling-irps.md)

[重复使用 Irp](reusing-irps.md)

[设备特定于类型的 I/O 请求](device-type-specific-i-o-requests.md)

[使用 I/O 控制代码](using-i-o-control-codes.md)

[使用 IRP 优先级提示](using-irp-priority-hints.md)

[IRP 主要函数代码](irp-major-function-codes.md)

[IRP 处理示例](irp-processing-examples.md)

 

 




