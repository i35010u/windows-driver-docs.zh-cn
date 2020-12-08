---
title: 浮点数到 XR_BIAS 转换规则
description: 浮点数到 XR_BIAS 转换规则
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，将 float 转换为 XR_BIAS
- 扩展格式 WDK Windows 7 显示，将 float 转换为 XR_BIAS
- 将 float 转换为 XR_BIAS WDK Windows 7 显示器
- float WDK Windows 7 显示
- float WDK Windows 7 显示，转换到 XR_BIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b11c2a02838dfe6bee77547358b9dc38477fc8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817389"
---
# <a name="float-to-xr_bias-conversion-rules"></a>Float to XR \_ 偏向转换规则


本部分仅适用于 Windows 7 及更高版本的操作系统。

以下规则适用于将 float 转换为 XR \_ 偏量。 在这些规则中，假定起始 float 值为 c。

-   如果 c 为 NaN，则结果为 0;否则，将应用以下规则。 NaN 代表 "不是数字"，这意味着表示一个值的符号实体，但该实体在浮点格式中不可用。

-   执行以下操作以从 float scale 转换为整数小数位数：

    c = c \* 510

    前面的操作可能会导致溢出。

-   为偏向执行以下操作：

    c = c + 384

    前面的操作可能会导致溢出。

-   根据 c 的指数，执行以下操作之一进行夹具操作：

    如果、后偏移、c 的指数大于或等于 2 (&gt; = 2 或 c 为 INF) ，则结果为0x3ff，这大约相当于1.2529。

    如果、post 偏量、c 的指数小于 0 (&lt; 0 或 c 为-INF) ，则结果为0x0，表示约-0.7529。

-   如果结果为，则重新解释 c 的尾数的最高有效10位。

Float 到 XR 偏向的转换 \_ 允许在 XR 端对 0.6 f Unit-Last (ulp 范围内) 的容差。 此容差意味着在从 float 转换为 XR 之后，允许表示支持的目标格式值的 0.6 f ULP 范围内中的任何值映射到该值。 请注意，对于无限精确的结果，ULP 范围内是指允许实现将结果截断为32位，而不是执行舍入到最接近的结果，因为这会导致最后一个 (最小) 位置中的一个单元出现在浮点数中的最小值。

还适用于反转数据的标准 Direct3D 版本10要求。

 

 





