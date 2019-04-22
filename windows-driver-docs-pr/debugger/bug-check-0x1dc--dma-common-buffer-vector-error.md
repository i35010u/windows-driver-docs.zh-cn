---
title: Bug 检查 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
description: DMA_COMMON_BUFFER_VECTOR_ERROR bug 检查具有 0x000001DC 值。 它指示该驱动程序已被误用 DMA 向量常见缓冲区 Api。
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
ms.openlocfilehash: 008bd282a92f17262aefff3400068796acb708fe
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238800"
---
# <a name="bug-check-0x1dc-dmacommonbuffervectorerror"></a>Bug 检查 0x1DC：DMA\_常见\_缓冲区\_向量\_错误

DMA\_常见\_缓冲区\_向量\_错误 bug 检查的值为 0x000001DC。 它指示驱动程序已被误用 DMA 向量常见缓冲区 Api。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="dmacommonbuffervectorerror-parameters"></a>DMA\_常见\_缓冲区\_向量\_错误参数

|参数|描述|
|-------- |---------- |
|1| 指示失败的类型。 请参阅下面的值。|
|2| 请参阅下面的值。 |
|3| 请参阅下面的值。 |
|4| 请参阅下面的值。 |

**失败的类型**

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

驱动程序已被误用 DMA 向量常见缓冲区 Api。

## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

