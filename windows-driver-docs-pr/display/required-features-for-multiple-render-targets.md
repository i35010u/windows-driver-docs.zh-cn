---
title: 多个渲染器目标的必需功能
description: 多个渲染器目标的必需功能
keywords:
- 呈现多个目标 WDK DirectX 9.0，必需的功能
- 多个呈现目标 WDK DirectX 9.0，必需的功能
- 同时呈现目标 WDK DirectX 9.0，必需的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9172db99d2c75815525f2d59104bc7c082183af4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799629"
---
# <a name="required-features-for-multiple-render-targets"></a>多个渲染器目标的必需功能


## <span id="ddk_required_features_for_multiple_render_targets_gg"></span><span id="DDK_REQUIRED_FEATURES_FOR_MULTIPLE_RENDER_TARGETS_GG"></span>


支持同时呈现到多个目标的 DirectX 9.0 版本驱动程序必须支持以下功能：

-   给定多个呈现器目标组的所有表面均以原子方式分配。 此限制的解决方法是将此限制视为具有多个 RGBA 通道交错的新类型的表面格式。

-   仅支持32位表面格式 (例如，RGBA8、RGBA10、U16V16 和 R32f 类型格式) 。 此限制以新的表面格式的名称表示。

-   多个呈现器目标组不能是主 (，即) 显示的图面。 多呈现器目标组必须仅在屏幕之外。 此限制通过表面格式枚举来表示。

-   多个呈现器目标组不能为 mipmap。 也就是说，创建 MIP 链将失败。

-   不能将多个呈现器目标组的元素设置为与呈现目标相同的纹理。 但组面的不同元素可以同时为纹理和呈现目标。

-   不支持多个呈现器目标组的抗锯齿。

-   无法筛选作为纹理使用的多个呈现器目标组的元素。 也就是说，任何取样器状态都不会影响 lookup。

-   无法锁定多个呈现器目标组的元素。

-   通过将每个元素分配给不同的阶段（如典型纹理），可以同时使用多个呈现器目标组的多个元素。

-   多个呈现器目标组的元素支持在读取时进行 gamma 2.2-1.0 转换，就像其他纹理格式一样。

-   D3DDP2OP \_ 清除操作代码将清除多个呈现器目标组的所有元素。

 

 





