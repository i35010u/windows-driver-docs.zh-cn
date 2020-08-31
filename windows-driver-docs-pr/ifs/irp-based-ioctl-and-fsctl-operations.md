---
title: 基于 IRP 的 IOCTL 和 FSCTL 操作
description: 基于 IRP 的 IOCTL 和 FSCTL 操作
ms.assetid: 08d6cf89-aaba-4aa1-baff-eb6aece2875f
keywords:
- IOCTLs WDK 文件系统
- FSCTL WDK 文件系统
- 无缓冲区 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd7ce44b9baf74fc32a33a00f1f857b567f40b5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063062"
---
# <a name="irp-based-ioctl-and-fsctl-operations"></a>基于 IRP 的 IOCTL 和 FSCTL 操作


## <span id="ddk_irp_based_ioctl_and_fsctl_operations_if"></span><span id="DDK_IRP_BASED_IOCTL_AND_FSCTL_OPERATIONS_IF"></span>


下面的基于 IRP 的 i/o 操作使用与 i/o 控制代码定义中指定的传输类型（ (IOCTL) 或文件系统控制代码） (FSCTL) 的缓冲方法：

-   IRP\_MJ\_DEVICE\_CONTROL

-   IRP \_ MJ \_ 文件 \_ 系统 \_ 控制

-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

在 CTL 代码宏的 *TransferType* 参数中指定传输类型 \_ 。 若要获取给定 IOCTL 或 FSCTL 的传输类型，请使用以下宏：

```cpp
#define METHOD_FROM_CTL_CODE(ctrlCode)         ((ULONG)(ctrlCode & 3))
```

此宏返回以下值之一：

```cpp
#define METHOD_BUFFERED                 0
#define METHOD_IN_DIRECT                1
#define METHOD_OUT_DIRECT               2
#define METHOD_NEITHER                  3
```

有关 CTL 代码宏的详细信息 \_ ，请参阅 [定义 I/o 控制代码](../kernel/defining-i-o-control-codes.md)。

请注意，IRP \_ MJ \_ 设备 \_ 控制也可以是一种快速的 i/o 操作。 当它是快速 i/o 操作时，不管 IOCTL 的传输类型如何，它都始终使用未缓冲和直接的 i/o。 若要详细了解 IRP \_ MJ \_ 设备 \_ 控制能否作为快速 i/o 操作，请参阅 [可以是基于 IRP 的操作或快速](operations-that-can-be-irp-based-or-fast-i-o.md)i/o。

 

