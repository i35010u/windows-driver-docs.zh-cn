---
title: Windows 8 显示驱动程序 (WDDM 1.2) 的新增功能
description: Windows 8 中的新增功能（用于显示驱动程序）。
keywords:
- Windows 8 WDK 显示的新增
- WDDM 1.2，Windows 8 WDK 显示新增
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6717f18e8207e3b4d163ac8d54ea518c39454b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826033"
---
# <a name="whats-new-for-windows-8-display-drivers-wddm-12"></a>Windows 8 显示驱动程序 (WDDM 1.2) 的新增功能


Windows 8 引入了 1.2 (WDDM) 版本的 Windows 显示驱动程序模型。 WDDM 1.2 还支持 Microsoft Direct3D 版本11.1。 请参阅以下主题，了解有关功能的信息、独立硬件供应商 (Ihv) 和硬件要求的指导：

<span id="wddm_1.2_and_windows_8"></span><span id="WDDM_1.2_AND_WINDOWS_8"></span>[WDDM 1.2 和 Windows 8](wddm-in-windows-8.md)  
WDDM 1.2 概述

<span id="wddm_1.2_features"></span><span id="WDDM_1.2_FEATURES"></span>[WDDM 1.2 功能](wddm-v1-2-features.md)  
WDDM 1.2 中提供的新功能的说明

请注意，这些要求也已添加到文档中：

## <a name="span-idsummary_of_direct3d_support_requirements__november_2012_spanspan-idsummary_of_direct3d_support_requirements__november_2012_spanspan-idsummary_of_direct3d_support_requirements__november_2012_spansummary-of-direct3d-support-requirements-november-2012"></a><span id="Summary_of_Direct3D_support_requirements__November_2012_"></span><span id="summary_of_direct3d_support_requirements__november_2012_"></span><span id="SUMMARY_OF_DIRECT3D_SUPPORT_REQUIREMENTS__NOVEMBER_2012_"></span>2012年11月 (的 Direct3D 支持要求摘要) 


以下主题列出了用户模式驱动程序必须支持的不同 Direct3D 功能级别的硬件功能和格式：

-   [Direct3D 功能级别的硬件支持](hardware-support-for-direct3d-feature-levels.md)

-   [必需的 Direct3D 9 功能](required-direct3d-9-capabilities.md)

-   [必需的 DXGI 格式](required-dxgi-formats.md)

## <a name="span-idcorrections_to_xr_bias_conversions__november_2012_spanspan-idcorrections_to_xr_bias_conversions__november_2012_spanspan-idcorrections_to_xr_bias_conversions__november_2012_spancorrections-to-xr_bias-conversions-november-2012"></a><span id="Corrections_to_XR_BIAS_conversions__November_2012_"></span><span id="corrections_to_xr_bias_conversions__november_2012_"></span><span id="CORRECTIONS_TO_XR_BIAS_CONVERSIONS__NOVEMBER_2012_"></span>更正 XR \_) 11 2012 月 (偏向转换


\_以下主题已更正了 XR 和 XR 偏向格式要求：

[XR 布局](xr-layout.md)

[XR \_ 偏向颜色通道转换规则](xr-bias-color-channel-conversion-rules.md)

[XR \_ 偏移转换规则](xr-bias-to-float-conversion-rules.md)

[Float to XR \_ 偏向转换规则](float-to-xr-bias-conversion-rules.md)

[从 BGR8888 到 XR 偏向的转换 \_](conversion-from-bgr8888-to-xr-bias.md)

 

 





