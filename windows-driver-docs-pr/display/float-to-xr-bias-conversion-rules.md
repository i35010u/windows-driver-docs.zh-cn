---
title: 浮点数到 XR_BIAS 转换规则
description: 浮点数到 XR_BIAS 转换规则
ms.assetid: 496306d5-7494-4df6-8af7-9acb0e2708f9
keywords:
- 将浮点数转换为 XR_BIAS 的 Direct3D 版本 10.1 WDK Windows 7 显示
- 扩展的格式 WDK Windows 7 显示，将 float 转换为 XR_BIAS
- 将浮点数转换为 XR_BIAS WDK Windows 7 显示
- float WDK Windows 7 显示
- float WDK Windows 7 显示，转换为 XR_BIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a855d755341496b15157eb769b214087e3f624ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338646"
---
# <a name="float-to-xrbias-conversion-rules"></a>向 XR 浮动\_偏置转换规则


本部分仅适用于 Windows 7 和更高版本的操作系统。

下列规则适用于将 float 转换为 XR\_偏置。 在这些规则中，假设起始的 float 值为 c。

-   如果 c 为 NaN，则结果为 0;否则，应用以下规则。 NaN 代表"不是数字，"这意味着符号实体的表示值不是以浮点格式。

-   执行以下操作以从 float 缩放转换为整数范围：

    c = c \* 510

    在上一操作可能会导致溢出。

-   执行偏差的以下操作：

    c = c + 384

    在上一操作可能会导致溢出。

-   执行以下操作要固定其范围，具体取决于 c： 指数之一

    如果 post 偏置，c 的指数是大于或等于 2 (&gt;= 2 或 c 是 INF)，结果是 0x3ff，这大约相当于 1.2529。

    如果 post 偏置，c 的指数小于 0 (&lt; 0 或 c 是-INF)，结果是 0x0，大约表示-0.7529。

-   将 c 的尾数的最明显的 10 位重新解释为结果中。

浮点型转换为 XR\_偏差允许容差为 0.6f 单元最后一个位置 （ulp 范围） XR 端。 此功能意味着从浮点型转换为 XR 之后, 0.6f 中的任何值 ulp 范围表示支持的目标格式值的允许将映射到此值。 请注意，可无限精确的结果的 1 ulp 范围意味着，例如，实现允许截断为 32 位的结果而不是执行轮-到-最近的-甚至是，与将导致错误的最多一个单元中的最后一个 （最不重要） 的位置表示的浮点数中。

反转数据的标准 Direct3D 版本 10 要求也适用。

 

 





