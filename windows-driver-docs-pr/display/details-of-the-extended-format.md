---
title: 扩展格式的详细信息
description: 扩展格式的详细信息
ms.assetid: e9cd2bc7-99c1-4aca-91b0-9faefa4a856d
keywords:
- 扩展格式的 Direct3D 版本 10.1 WDK Windows 7 显示
- 扩展格式 WDK Windows 7 的显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1983f4c5acfde48a2051a00e450df326ab3187
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563923"
---
# <a name="details-of-the-extended-format"></a>扩展格式的详细信息


本部分仅适用于 Windows 7 和更高版本的操作系统。

下表中的格式名称 XR 一部分可被视为类似于 UNORM 或圣位的新的着色器解释。 XR\_偏差一部分格式名称是一种特殊情况以重载此语义具有其他元数据的解释。 此元数据指示格式必须可显式偏移量和转换入和移出着色器的着色器代码中有偏差。 该驱动程序不需要执行任何此 biasing 工作;它完全留给应用程序。

下表显示了具有特定特性，供扩展的格式，如果硬件支持这些扩展的格式具有这些属性的资源，或者如果扩展格式的这些资源都是可选的资源。

格式 (DXGI\_格式\_\*) B8G8R8A8 B8G8R8A8 B8G8R8X8 B8G8R8X8 R10G10B10 资源 B8G8R8A8 \_UNORM \_UNORM B8G8R8X8 \_UNORM \_UNORM R10G10B10A2 \_XR\_偏置特性\_TYPELESS （现有） \_SRGB \_TYPELESS （现有） \_SRGB \_TYPELESS \_A2\_UNORM 缓冲区

不可用

R

（更改）

不可用

不可用

R

（更改）

不可用

不可用

不可用

Input

组装器

顶点

缓冲区

不可用

R

（更改）

不可用

不可用

R

（更改）

不可用

不可用

不可用

Texture1D

R

R

（更改）

R

R

R

（更改）

R

R

不可用

Texture2D

R

R

（更改）

R

R

R

R

R

R

Texture3D

R

R

（更改）

R

R

R

（更改）

R

R

不可用

纹理

多维数据集

R

R

（更改）

R

R

R

（更改）

R

R

不可用

着色器 ID

不可用

R

R

不可用

R

R

不可用

不可用

着色器

示例

（任何筛选器）

不可用

R

R

不可用

R

R

不可用

不可用

MIP-map

纹理

R

R

（更改）

R

R

R

（更改）

R

R

不可用

MIP-map

自动-

生成

不可用

R

（更改）

R

不可用

R

（更改）

R

不可用

不可用

呈现

目标

不可用

R

R

不可用

R

R

不可用

不可用

Blendable

呈现

目标

不可用

R

R

不可用

R

R

不可用

不可用

CPU

可锁定

R

R

R

R

R

R

R

R

多-

示例

呈现

目标

不可用

O

O

不可用

o

o

不可用

不可用

多-

示例

解决

不可用

R

（更改）

R

不可用

R

（更改）

R

不可用

不可用

多-

示例

加载

不可用

R

R

不可用

R

R

不可用

不可用

显示

扫描出

不可用

R

（更改）

R

不可用

不可用

不可用

不可用

R

强制转换

在位

布局

R

R

（更改）

R

R

R

R

R

R

 

**请注意**  上表中单元格条目具有以下含义：
-   "R"表示需要硬件支持

-   "o"表示硬件支持是可选项

-   N/A 指示资源属性不是适用于扩展格式中，或不允许扩展的格式

 

**请注意**   DXGI\_格式\_B8G8R8A8\_UNORM 和 DXGI\_格式\_B8G8R8X8\_DXGI 中已存在 UNORM 格式\_格式的枚举。 但是，它们现在被视为相应的新系列的成员。 其要求已更改为其原始定义进行比较。

 

**请注意**  的"输入装配器索引缓冲区，"行"着色器示例\_c （比较筛选器）"，在不包括"着色器示例 （mono 1 位筛选器）"、"着色器 gather4"和"深度模具目标"资源属性前面的表，以提高可读性。 所有这些资源属性的含义是不适用。

 

以下部分介绍了新的扩展格式的详细信息：

[XR 布局](xr-layout.md)

[XR 格式 Alpha 内容](xr-format-alpha-content.md)

[DXGI\_FORMAT\_R10G10B10\_XR\_BIAS\_A2\_UNORM](dxgi-format-r10g10b10-xr-bias-a2-unorm.md)

[强制转换 XR 格式的能力](casting-ability-of-xr-formats.md)

[XR\_偏差颜色通道转换规则](xr-bias-color-channel-conversion-rules.md)

[X 通道的解释](interpretation-of-x-channel.md)

 

 





