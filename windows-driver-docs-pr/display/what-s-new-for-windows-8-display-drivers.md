---
title: 什么是 Windows 8 显示器驱动程序 (WDDM 1.2) 的新增功能
ms.assetid: E2EE9B0A-B9EA-4073-ACF0-2B8CC00760FC
description: 有关 Windows 8 中的新功能显示驱动程序。
keywords:
- Windows 8 WDK 显示的新增功能
- WDDM 1.2，Windows 8 WDK 显示的新增功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15c66765571f261dbbee3015d241574b4b736127
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533684"
---
# <a name="whats-new-for-windows-8-display-drivers-wddm-12"></a>什么是 Windows 8 显示器驱动程序 (WDDM 1.2) 的新增功能


Windows 8 引入了 Windows 显示器驱动程序模型 (WDDM) 1.2 版。 WDDM 1.2 还支持 Microsoft Direct3D 版本 11.1。 有关功能、 独立硬件供应商 (Ihv) 和硬件要求的指南，请参阅这些主题信息：

<span id="wddm_1.2_and_windows_8"></span><span id="WDDM_1.2_AND_WINDOWS_8"></span>[WDDM 1.2 和 Windows 8](wddm-in-windows-8.md)  
WDDM 1.2 的概述

<span id="wddm_1.2_features"></span><span id="WDDM_1.2_FEATURES"></span>[WDDM 1.2 功能](wddm-v1-2-features.md)  
WDDM 1.2 中提供的新功能的说明

请注意这些也已添加到文档的要求：

## <a name="span-idsummaryofdirect3dsupportrequirementsnovember2012spanspan-idsummaryofdirect3dsupportrequirementsnovember2012spanspan-idsummaryofdirect3dsupportrequirementsnovember2012spansummary-of-direct3d-support-requirements-november-2012"></a><span id="Summary_of_Direct3D_support_requirements__November_2012_"></span><span id="summary_of_direct3d_support_requirements__november_2012_"></span><span id="SUMMARY_OF_DIRECT3D_SUPPORT_REQUIREMENTS__NOVEMBER_2012_"></span>Direct3D 支持要求 (2012 年 11 月) 的摘要


这些主题列出的硬件功能和格式的用户模式驱动程序必须支持为不同的 Direct3D 功能级别：

-   [Direct3D 功能级别的硬件支持](hardware-support-for-direct3d-feature-levels.md)

-   [所需的 Direct3D 9 功能](required-direct3d-9-capabilities.md)

-   [所需的 DXGI 格式](required-dxgi-formats.md)

## <a name="span-idcorrectionstoxrbiasconversionsnovember2012spanspan-idcorrectionstoxrbiasconversionsnovember2012spanspan-idcorrectionstoxrbiasconversionsnovember2012spancorrections-to-xrbias-conversions-november-2012"></a><span id="Corrections_to_XR_BIAS_conversions__November_2012_"></span><span id="corrections_to_xr_bias_conversions__november_2012_"></span><span id="CORRECTIONS_TO_XR_BIAS_CONVERSIONS__NOVEMBER_2012_"></span>更正 XR\_偏置转换 (2012 年 11 月)


XR 和 XR\_偏差格式要求已经得到更正这些主题中：

[XR 布局](xr-layout.md)

[XR\_偏差颜色通道转换规则](xr-bias-color-channel-conversion-rules.md)

[XR\_偏置浮动的转换规则](xr-bias-to-float-conversion-rules.md)

[向 XR 浮动\_偏置转换规则](float-to-xr-bias-conversion-rules.md)

[从 BGR8888 转换为 XR\_偏差](conversion-from-bgr8888-to-xr-bias.md)

 

 





