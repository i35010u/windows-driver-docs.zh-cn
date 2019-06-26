---
title: 基于 IRP 的 IOCTL 和 FSCTL 操作
description: 基于 IRP 的 IOCTL 和 FSCTL 操作
ms.assetid: 08d6cf89-aaba-4aa1-baff-eb6aece2875f
keywords:
- Ioctl WDK 文件系统
- FSCTL WDK 文件系统
- 没有缓冲区 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1106fef7d2c48024f28dc2a33136545a853fb0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384568"
---
# <a name="irp-based-ioctl-and-fsctl-operations"></a>基于 IRP 的 IOCTL 和 FSCTL 操作


## <span id="ddk_irp_based_ioctl_and_fsctl_operations_if"></span><span id="DDK_IRP_BASED_IOCTL_AND_FSCTL_OPERATIONS_IF"></span>


以下基于 IRP 的 I/O 操作使用缓冲 I/O 控制代码 (IOCTL) 或文件系统的控制代码 (FSCTL) 的定义中指定的传输类型匹配的方法：

-   IRP\_MJ\_DEVICE\_CONTROL

-   IRP\_MJ\_FILE\_SYSTEM\_CONTROL

-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

中指定的传输类型*留空，则*CTL 参数\_代码宏。 若要获取给定 IOCTL 或 FSCTL 传输类型，请使用以下宏：

```cpp
#define METHOD_FROM_CTL_CODE(ctrlCode)         ((ULONG)(ctrlCode & 3))
```

此宏将返回以下值之一：

```cpp
#define METHOD_BUFFERED                 0
#define METHOD_IN_DIRECT                1
#define METHOD_OUT_DIRECT               2
#define METHOD_NEITHER                  3
```

详细了解 CTL\_代码宏，请参阅[定义的 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。

请注意该 IRP\_MJ\_设备\_控件也可以是一个快速的 I/O 操作。 快速的 I/O 操作时，它始终使用既不缓冲，也不直接 I/O，而不考虑 IOCTL 的传输类型。 有关详细信息，有关何时 IRP\_MJ\_设备\_控件可以是一个快速的 I/O 操作，请参阅[基于可以为 IRP 的操作或快速 I/O](operations-that-can-be-irp-based-or-fast-i-o.md)。

 

 




