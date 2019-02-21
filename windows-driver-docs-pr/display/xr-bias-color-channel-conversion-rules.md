---
title: XR_BIAS 颜色通道转换规则
description: XR_BIAS 颜色通道转换规则
ms.assetid: B3014241-A86A-4B6E-BC9D-50057B924D98
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49f073b4c9a5dc1e4a8d471f1d36db87c59c3756
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534815"
---
# <a name="xrbias-color-channel-conversion-rules"></a>XR\_偏差颜色通道转换规则


本部分仅适用于 Windows 7 和更高版本的操作系统。

这些主题提供 XR 之间进行转换的要求\_偏差和其他颜色通道：

[XR\_偏置浮动的转换规则](xr-bias-to-float-conversion-rules.md)

[向 XR 浮动\_偏置转换规则](float-to-xr-bias-conversion-rules.md)

[从 BGR8888 转换为 XR\_偏差](conversion-from-bgr8888-to-xr-bias.md)

以下是一些示例转换值使用的转换规则：

| 帧缓冲区值 | 解释 |
|--------------------|----------------|
| 000 = 0x000        | -0.7529        |
| 129 = 0x081        | -0.5000        |
| 384 = 0x180        | 0.0000         |
| 639 = 0x27f        | 0.5000         |
| 894 = 0x37e        | 1.0000         |
| 1023 = 0x3ff       | 1.2529         |

 

 

 





