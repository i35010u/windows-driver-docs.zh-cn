---
title: XR_BIAS 颜色通道转换规则
description: 介绍 XR_BIAS 颜色通道转换规则
ms.assetid: B3014241-A86A-4B6E-BC9D-50057B924D98
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3367e56b2943b39278bcda7433517271a35cb2df
ms.sourcegitcommit: 89b8a43480246dd726e3632aab2db9cf2eb7505d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92254024"
---
# <a name="xr_bias-color-channel-conversion-rules"></a>XR_BIAS 颜色通道转换规则

本部分适用于 Windows 7 及更高版本的操作系统。

以下主题提供了在 XR_BIAS 与其他颜色通道之间进行转换的要求：

* [XR_BIAS 到浮点数转换规则](xr-bias-to-float-conversion-rules.md)

* [浮点数到 XR_BIAS 转换规则](float-to-xr-bias-conversion-rules.md)

* [从 BGR8888 转换为 XR_BIAS](conversion-from-bgr8888-to-xr-bias.md)

下面是使用转换规则的一些示例转换值：

| 帧缓冲区值 | 解释 |
|--------------------|----------------|
| 000 = 0x000        | -0.7529        |
| 129 = 0x081        | -0.5000        |
| 384 = 0x180        | 0.0000         |
| 639 = 0x27f        | 0.5000         |
| 894 = 0x37e        | 1.0000         |
| 1023 = 0x3ff       | 1.2529         |
