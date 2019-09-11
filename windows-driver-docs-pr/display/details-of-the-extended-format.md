---
title: 扩展格式的详细信息
description: 扩展格式的详细信息
ms.assetid: e9cd2bc7-99c1-4aca-91b0-9faefa4a856d
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，扩展格式
- 扩展格式 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 137f4763413bcd2c3ba555ca2c9da76b21d4460b
ms.sourcegitcommit: 9b0ddcdba8c56987b45e538948b2ac8c60ef1287
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70876925"
---
# <a name="details-of-the-extended-format"></a>扩展格式的详细信息

本部分仅适用于 Windows 7 及更高版本的操作系统。

在下表中，格式名称的 XR 部分可以被视为类似于 UNORM 或圣马丁的位的新着色器解释。 格式名\_的 XR 偏向部分是一种特殊情况，它重载了包含其他元数据的语义。 此元数据指示格式必须在着色器代码中显式偏移并偏向，并在着色器中进行转换。 此驱动程序无需执行任何此使工作;它完全留给了应用程序。

## <a name="table-of-extended-formats"></a>扩展格式表

下表显示了在硬件为具有这些属性的资源支持这些扩展格式，或者这些资源的扩展格式为可选时，具有使用扩展格式的特定属性的资源。

<table>
<head>
    <tr>
        <th colspan="9">Formats （DXGI_FORMAT_ *）</th>
    </tr>
    <tr>
        <th></th>
        <th></th>
        <th>B8G8R8A8</th>
        <th>B8G8R8A8</th>
        <th></th>
        <th>B8G8R8X8</th>
        <th>B8G8R8X8</th>
        <th></th>
        <th>R10G10B10</th>
    </tr>
    <tr>
        <th>Resource</th>
        <th>B8G8R8A8</th>
        <th>_UNORM</th>
        <th>_UNORM</th>
        <th>B8G8R8X8</th>
        <th>_UNORM</th>
        <th>_UNORM</th>
        <th>R10G10B10A2</th>
        <th>_XR_BIAS</th>
    </tr>
    <tr>
        <th>属性</th>
        <th>_TYPELESS</th>
        <th>现存</th>
        <th>_SRGB</th>
        <th>_TYPELESS</th>
        <th>现存</th>
        <th>_SRGB</th>
        <th>_TYPELESS</th>
        <th>_A2_UNORM</th>
    </tr>
</head>
<body>
    <tr>
        <td>缓冲区</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>输入汇编程序顶点缓冲区</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>Texture1D</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>Texture2D</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
    </tr>    <tr>
        <td>Texture3D</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>纹理多维数据集</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>着色器 ID</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>着色器示例（任何筛选器）</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>MIP-地图纹理</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>MIP-映射自动生成</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>呈现目标</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>Blendable 呈现目标</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>CPU 锁定</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
    </tr>
    <tr>
        <td>多示例呈现器目标</td>
        <td>不可用</td>
        <td>O</td>
        <td>O</td>
        <td>不可用</td>
        <td>O</td>
        <td>O</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>多示例解析</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>多示例负载</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>R</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
    </tr>
    <tr>
        <td>显示扫描</td>
        <td>不可用</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>不可用</td>
        <td>R</td>
    </tr>
    <tr>
        <td>位布局内的强制转换</td>
        <td>R</td>
        <td>R （已更改）</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
    </tr>
</body>
</table>

>[!NOTE]
>在上表中，单元条目具有以下含义：
>
>- "R" 表示需要硬件支持
>- "o" 表示硬件支持是可选的
>- "否" 表示资源属性不适用于扩展格式或不允许使用扩展格式

>[!NOTE]
>Dxgi 格式\_枚举\_中\_\_\_\_已经存在 dxgi format B8G8R8A8 UNORM 和 dxgi format B8G8R8X8 UNORM 格式。\_ 但是，它们现在被视为适当的新系列的成员。 与原始定义相比，它们的要求已经发生了变化。

>[!NOTE]
>上表中未包含 "输入汇编程序索引缓冲区"、"\_着色器示例 c （比较筛选器）"、"着色器示例（mono 1 位筛选器）"、"着色器 gather4" 和 "深度模具目标" 资源属性的行，以方便阅读。 这些资源属性的所有含义均为 N/A。

以下各节介绍了新扩展格式的详细信息：

[XR 布局](xr-layout.md)

[XR 格式 Alpha 内容](xr-format-alpha-content.md)

[DXGI\_FORMAT\_R10G10B10XR\_偏向\_A2UNORM\_\_](dxgi-format-r10g10b10-xr-bias-a2-unorm.md)

[XR 格式的强制转换能力](casting-ability-of-xr-formats.md)

[XR\_偏向颜色通道转换规则](xr-bias-color-channel-conversion-rules.md)

[X 通道的解释](interpretation-of-x-channel.md)
