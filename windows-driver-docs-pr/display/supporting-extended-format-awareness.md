---
title: 支持扩展格式感知
description: 支持扩展格式感知
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示
- Direct3D 版本 10.1 WDK Windows 7 显示，扩展格式感知
- 扩展格式感知 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d9e3c8da1abf1f8181b6af97bad5420b196d269
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789959"
---
# <a name="supporting-extended-format-awareness"></a>支持扩展格式感知


本部分仅适用于 Windows 7 及更高版本的操作系统。

为 Windows 7 提供的 Direct3D 10.1 版本定义了几种新格式。 此外，Windows 7 Direct3D 10.1 提供了 DXGI \_ 格式 \_ R8G8B8A8 的无 \_ 类型现有格式系列，可以在成员之间进行转换。 Direct3D 10.1 和更高版本通过新版本和硬件功能发现机制公开此扩展格式支持。 即使图形硬件具有 Direct3D 10.1 功能，Direct3D 10.0 也不支持扩展格式。

以下是支持扩展格式感知的新 Direct3D 10.1 功能：

-   用于高颜色扫描的新 XR 格式

-   重新添加 Direct3D 版本10中缺少的 BGR 格式

-   启用为 DXGI 格式的完全类型成员创建不同格式的视图 R8G8B8A8 无 \_ 类型 \_ \_ ，dxgi \_ 格式 R10G10B10A2 无 \_ 类型 \_ 和 dxgi \_ 格式 \_ R16G16B16 答16无类型 \_ \_ 族，其中包含所有 Direct3D 版本10扫描输出格式

-   BGRA 和 BGRA SRGB 的扫描和提供支持 \_

Windows 7 还向其版本提供了一个新的交换链标志，该标志允许10:10:10:2 后台缓冲区的 XR 解释与 DWM 通信。

以下部分介绍了 Direct3D 的新功能：

[版本发现支持](version-discovery-support.md)

[扩展格式的详细信息](details-of-the-extended-format.md)

[完全类型化后端缓冲区强制转换](fully-typed-back-buffers-casting.md)

[BGRA 扫描输出支持](bgra-scan-out-support.md)

[扩展格式感知要求](extended-format-aware-requirements.md)

[Direct3D 版本 9 驱动程序的 DDI 更改](ddi-changes-for-direct3d-version-9-drivers.md)

 

 





