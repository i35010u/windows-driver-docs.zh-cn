---
title: Bug 检查 0x1A4 DRIPS_SW_HW_DIVERGENCE_LIVEDUMP
description: DRIPS_SW_HW_DIVERGENCE_LIVEDUMP 的实时转储的值为0x000001A4。
keywords:
- Bug 检查 0x1A4 DRIPS_SW_HW_DIVERGENCE_LIVEDUMP
- DRIPS_SW_HW_DIVERGENCE_LIVEDUMP
ms.date: 05/25/2018
topic_type:
- apiref
api_name:
- DRIPS_SW_HW_DIVERGENCE_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0bdbb484f1a0bdc492585ccacd5d8dc7aaf21a8b
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852094"
---
# <a name="bug-check-0x1a4-drips_sw_hw_divergence_livedump"></a>Bug 检查0x1A4： DRIPS \_ SW \_ HW \_ 发散 \_ LIVEDUMP 

DRIPS \_ SW \_ HW \_ 发散 \_ LIVEDUMP 实时转储的值为0x000001A4。 

软件和硬件 DRIPS 的分歧超过了默认/程控阈值时间。

（此代码永远不能用于实际错误检查; 它用于标识实时转储。）

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="drips_sw_hw_divergence_livedump-parameters"></a>DRIPS \_ SW \_ HW \_ 发散 \_ LIVEDUMP 参数


以下参数显示在蓝色屏幕上。

参数 | 说明 
|---------|--------------|
1 | 软件 DRIPS 所用的时间（微秒）。
2 |  硬件 DRIPS 所用的时间（微秒）。
3 |  保留。
4 |  保留。

 

 




