---
title: 扩展的格式感知提供支持
description: 扩展的格式感知提供支持
ms.assetid: b473ebf2-75a0-4e3f-8190-d1a557ae6da0
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示
- 扩展格式意识的 Direct3D 版本 10.1 WDK Windows 7 显示
- 扩展的格式感知 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54a7815037d84009221ab2dc2309a3e144e0f95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554539"
---
# <a name="supporting-extended-format-awareness"></a>扩展的格式感知提供支持


本部分仅适用于 Windows 7 和更高版本的操作系统。

版本的 Windows 7 提供的 Direct3D 10.1 定义几个新的格式。 此外，Windows 7 Direct3D 10.1 提供 DXGI\_格式\_R8G8B8A8\_无类型与成员之间强制转换的功能的现有格式系列。 Direct3D 10.1 及更高版本公开新的版本和硬件功能发现机制通过此扩展的格式支持。 Direct3D 10.0 不支持扩展的格式，即使图形硬件具有 Direct3D 10.1 功能。

新的 Direct3D 10.1 功能以支持扩展的格式感知如下：

-   新 XR 高颜色扫描出格式

-   重新添加 BGR 格式所没有的 Direct3D 版本 10

-   启用创建以不同的方式格式化视图的完全类型化成员的 DXGI\_格式\_R8G8B8A8\_TYPELESS、 DXGI\_格式\_R10G10B10A2\_TYPELESS 和 DXGI\_格式\_R16G16B16\_答 16\_无类型系列，其中包含所有 Direct3D 版本 10 扫描扩展格式

-   扫描扩展并提供对 BGRA 和 BGRA 支持\_SRGB

Windows 7 还提供了它的 Direct3D 9 到 DWM 允许 10:10:10:2 后台缓冲区进行通信的 XR 解释的新交换链标志的版本。

以下各节介绍的 Direct3D 的新功能：

[版本发现支持](version-discovery-support.md)

[扩展格式的详细信息](details-of-the-extended-format.md)

[强制转换的完全类型化的后台缓冲区](fully-typed-back-buffers-casting.md)

[BGRA 扫描扩展支持](bgra-scan-out-support.md)

[扩展格式识别要求](extended-format-aware-requirements.md)

[DDI 更改为 9 的 Direct3D 版本的驱动程序的](ddi-changes-for-direct3d-version-9-drivers.md)

 

 





