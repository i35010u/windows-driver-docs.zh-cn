---
title: 桌面复制
description: Windows 8 引入了新的 Microsoft DirectX 图形基础结构 (DXGI) 的 API，使独立软件供应商 (Isv) 支持桌面协作和远程桌面访问方案。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5056a280c7e1d7eac9b0d76b9696c65a68ed9d9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809557"
---
# <a name="desktop-duplication"></a>桌面复制


Windows 8 引入了新的 Microsoft DirectX 图形基础结构 (DXGI) 的 API，使独立软件供应商 (Isv) 支持桌面协作和远程桌面访问方案。

此类应用程序广泛用于企业和培训方案。 这些应用程序共用一种常见要求：访问桌面内容以及将内容传输到远程位置的能力。 Windows 8 桌面复制 Api 提供对桌面内容的访问权限。

目前，无 Windows API 允许应用程序无缝实现此方案。 因此，应用程序使用镜像驱动程序、屏幕废弃和其他专用方法来访问桌面的内容。 但是，这些方法具有以下限制：

-   优化性能可能会很困难。
-   这些解决方案可能不支持更新的图形呈现 Api，因为在产品交付后会发布 Api。
-   Windows 不会始终提供丰富的元数据来帮助进行优化。
-   并非所有解决方案都与 Windows Vista 和更高版本的 Windows 中的桌面合成兼容。

Windows 8 引入了一种基于 DXGI 的 API，称为 *桌面复制 api*。 此 API 通过使用位图和关联的元数据进行优化，提供对桌面内容的访问。 此 API 适用于启用了 Aero 主题，不依赖于应用程序使用的图形 API。 如果用户可以在本地控制台上查看该应用程序，则也可以远程查看该内容。 这意味着甚至可以重复全屏显示的 DirectX 应用程序。 请注意，API 提供对访问受保护视频内容的保护。

利用 API，应用程序可以请求 Windows，以提供对桌面内容的访问，同时还提供监视器边界。 应用程序可以复制一个或多个活动显示。 当应用程序请求复制时，将发生以下情况：

-   Windows 呈现桌面，并向应用程序提供副本。
-   每个呈现的帧都置于 GPU 内存中。
-   每个呈现的帧都具有以下元数据：
    -   脏区域
    -   屏幕到屏幕移动
    -   鼠标光标信息
-   向应用程序提供对帧和元数据的访问权限。
-   应用程序负责处理每个帧：
    -   应用程序可以选择根据脏区域进行优化。
    -   应用程序可以选择使用硬件加速来处理移动和鼠标数据。
    -   在流式传输之前，应用程序可以选择使用硬件加速进行压缩。

有关详细的文档和示例，请参阅 [桌面复制 API](/windows/desktop/direct3ddxgi/desktop-dup-api)。

 

