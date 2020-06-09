---
title: Bug 检查 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
description: DMA_COMMON_BUFFER_VECTOR_ERROR bug 检查的值为0x000001DC。 它表示驱动程序误用了 DMA 向量公共缓冲 Api。
keywords:
- Bug 检查 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
- DMA_COMMON_BUFFER_VECTOR_ERROR
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- DMA_COMMON_BUFFER_VECTOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 140a35037a32191fae10658e1ae6d5ba94d5ede1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534828"
---
# <a name="bug-check-0x1dc-dma_common_buffer_vector_error"></a>Bug 检查0x1DC： DMA \_ 常见 \_ 缓冲区 \_ 向量 \_ 错误

DMA \_ 公共 \_ 缓冲区 \_ 向量 \_ 错误检查的值为0x000001DC。 它表示驱动程序误用了 DMA 向量公共缓冲 Api。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="dma_common_buffer_vector_error-parameters"></a>DMA \_ 常见 \_ 缓冲区 \_ 向量 \_ 错误参数

|参数|说明|
|-------- |---------- |
|1| 指示失败的类型。 请参阅下面的值。|
|2| 请参阅下面的值。 |
|3| 请参阅下面的值。 |
|4| 请参阅下面的值。 |

**失败类型**

```text
0x01 : Wrong IRQL
    2 - Current IRQL.

x02 : Vector not empty.
    2 - Index of remaining buffer.
    3 - Virtual Address of remaining buffer.
    4 - Logical address of remaining buffer.

0x03 : Index out of bounds.
    2 - Number of available entries.
    3 - Index requested.

0x04 : Index freed.
    2 - Index requested.

0x05 : Common buffer leaked.
```

## <a name="cause"></a>原因
-----

驱动程序误用了 DMA 向量公共缓冲 Api。 [**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

