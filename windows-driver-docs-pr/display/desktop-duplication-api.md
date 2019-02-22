---
title: 桌面的重复项
description: Windows 8 引入了新的基于 Microsoft DirectX 图形基础结构 DXGI 的 API，使独立软件供应商 (Isv) 以支持桌面协作和远程桌面访问方案轻松。
ms.assetid: 5D4CBEA1-3C13-4B5C-A43D-7E6DBBB1A80F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7b9e7d6792d60a231da694ff409c7e502a734a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555892"
---
# <a name="desktop-duplication"></a>桌面的重复项


Windows 8 引入了新的基于 Microsoft DirectX 图形基础结构 DXGI 的 API，使独立软件供应商 (Isv) 以支持桌面协作和远程桌面访问方案轻松。

在企业和教育方案广泛用于此类应用程序。 这些应用程序共享一个常见的要求： 对桌面以及用于传输到远程位置的内容的功能的内容的访问。 Windows 8 桌面复制 Api 提供对桌面的内容的访问。

目前，没有 Windows API 允许应用程序无缝地实现此方案。 因此，应用程序使用镜像驱动程序、 屏幕废弃，和其他专有方法来访问桌面的内容。 但是，这些方法具有以下一组的限制：

-   它极具挑战性来优化性能。
-   这些解决方案可能不支持较新的图形呈现 Api，因为 Api 发布后交付产品。
-   Windows 无法始终提供丰富的元数据来帮助进行优化。
-   并非所有解决方案都都与在 Windows Vista 和更高版本的 Windows 桌面组合兼容。

Windows 8 引入了一个称为基于 DXGI 的 API *Desktop 重复 API*。 此 API 提供对桌面的内容访问使用优化的位图和关联的元数据。 此 API 与 Aero 主题启用，并且不依赖于图形 API 的应用程序使用。 如果用户可以在本地控制台上查看该应用程序，然后可以从远程和查看内容。 这意味着该甚至全屏 DirectX 应用程序可以进行复制。 请注意该 API 提供了针对访问受保护的视频内容保护。

此 API 支持应用程序请求 Windows 以提供对桌面沿着监视器边界的内容的访问。 应用程序可以复制一个或多个活动的显示。 当应用程序请求重复时，将发生以下情况：

-   Windows 将呈现在桌面上，并提供到应用程序的副本。
-   每个呈现的帧位于 GPU 内存中。
-   每个呈现的帧附带以下元数据：
    -   已更新区域
    -   屏幕间移动
    -   鼠标光标信息
-   应用程序提供对帧和元数据的访问。
-   应用程序负责处理每个帧：
    -   应用程序可以选择优化基于已更新区域。
    -   应用程序可以选择使用硬件加速来处理数据移动和鼠标数据。
    -   应用程序可以选择要用于压缩，再流出的硬件加速。

有关详细的文档和示例，请参阅[Desktop 重复 API](https://msdn.microsoft.com/library/windows/desktop/hh404487)。

 

 





