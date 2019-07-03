---
title: Bug 检查 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
description: KERNEL_PARTITION_REFERENCE_VIOLATION bug 检查具有 0x0000018E 值。
keywords:
- Bug 检查 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
- KERNEL_PARTITION_REFERENCE_VIOLATION
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- KERNEL_PARTITION_REFERENCE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86603fb969f95ccf0fcf875a517f4e8abcc8f2b7
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519838"
---
# <a name="bug-check-bug-check-0x18e-kernelpartitionreferenceviolation"></a>Bug 检查 Bug 检查 0x18E:内核\_分区\_引用\_冲突

KERNEL_PARTITION_REFERENCE_VIOLATION bug 检查具有 0x0000018E 值。 

此错误指示分区已取消引用不正确。 这通常发生在内核模式驱动程序不会正确地取消引用分区对象。 它也会发生严重数据损坏时在内核中。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kernelpartitionreferenceviolation-parameters"></a>内核\_分区\_引用\_冲突参数

在蓝色屏幕上显示以下参数。

参数 1 指示失败的类型。 其他参数的含义取决于参数 1 的值。

参数 1 | 参数 2 | 参数 3 | 参数 4
|-----------|-------------|-------------|-------------|
| 0x0:正在删除具有非零值硬引用计数的分区。 | 对分区的指针。 | 未完成的硬引用数。 | 保留|
| 0x1:正在删除系统分区 | 对分区的指针。 | 保留 | 保留 |
| 0x2:正在删除具有未完成的 ex 工作队列项的分区。 | 对分区的指针。 |指向异常工作队列具有未完成的项目。 | 保留 |
 






