---
title: Bug 检查 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
description: KERNEL_PARTITION_REFERENCE_VIOLATION bug 检查的值为0x0000018E。
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
ms.openlocfilehash: 0142d57396cc4e980a30a7b4264970e5ecc67647
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852317"
---
# <a name="bug-check-0x18e-kernel_partition_reference_violation"></a>Bug 检查0x18E：内核 \_ 分区 \_ 引用 \_ 冲突

KERNEL_PARTITION_REFERENCE_VIOLATION bug 检查的值为0x0000018E。 

此错误表示分区未正确取消引用。 当内核模式驱动程序无法正确取消引用分区对象时，通常会发生这种情况。 如果内核中出现严重的数据损坏，也会出现这种情况。


> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kernel_partition_reference_violation-parameters"></a>内核 \_ 分区 \_ 引用 \_ 冲突参数

以下参数显示在蓝色屏幕上。

参数1指示失败的类型。 其他参数的意义取决于参数1的值。

参数 1 | 参数2 | 参数3 | 参数4
|-----------|-------------|-------------|-------------|
| 0x0：正在删除包含非零硬引用计数的分区。 | 指向分区的指针。 | 未完成的硬引用的数目。 | 保留|
| 0x1：正在删除系统分区 | 指向分区的指针。 | 保留 | 保留 |
| 0x2：正在删除包含未完成的 ex 工作队列项的分区。 | 指向分区的指针。 |指向包含未处理项的 ex 工作队列的指针。 | 保留 |
 






