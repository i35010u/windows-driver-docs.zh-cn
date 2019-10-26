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
ms.openlocfilehash: 16c5a8a24e70756d33305902c10ec54077aabd03
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916227"
---
# <a name="bug-check-0x1dc-dma_common_buffer_vector_error"></a>Bug 检查0x1DC： DMA\_常见\_缓冲区\_向量\_错误

DMA\_常见\_缓冲区\_向量\_错误 bug 检查的值为0x000001DC。 它表示驱动程序误用了 DMA 向量公共缓冲 Api。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="dma_common_buffer_vector_error-parameters"></a>DMA\_常见\_缓冲区\_向量\_错误参数

|参数|描述|
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

驱动程序误用了 DMA 向量公共缓冲 Api。 [ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码引用](bug-check-code-reference2.md)

