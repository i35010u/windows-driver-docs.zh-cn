---
title: 符合 DXGI DDI
description: 符合 DXGI DDI
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，DXGI DDI 一致性
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，DXGI DDI 一致性
- DirectX 图形基础结构 DDI 一致性 WDK Windows 7 显示
- DirectX 图形基础结构 DDI 一致性 WDK Windows Server 2008 R2 显示
- DXGI DDI 一致性 WDK Windows 7 显示
- DXGI DDI 一致性 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa5fd9b89304861fee010926962945a4b94e8c92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810177"
---
# <a name="conforming-to-the-dxgi-ddi"></a>符合 DXGI DDI


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

Direct3D 版本 11 DDI 符合 [DirectX 图形基础结构 (DXGI) DDI 的](directx-graphics-infrastructure-ddi.md) 资源接口定义、设备枚举和演示。

### <a name="span-idpresentationspanspan-idpresentationspanpresentation"></a><span id="presentation"></span><span id="PRESENTATION"></span>呈现

由于 Direct3D 版本11设备必须支持任何支持扫描的格式的表示形式，因此，用户模式显示的驱动程序将需要通过其显示的微型端口驱动程序 (内核模式驱动程序的显示操作，) 该驱动程序调用从任何扫描格式转换为任何其他扫描格式的颜色转换，以及标准的 GDI 扫描格式。 这些扫描格式由 DXGI 格式枚举中的以下值识别 \_ ：

-   DXGI \_ FORMAT \_ B5G6R5 \_ UNORM

-   DXGI \_ FORMAT \_ B5G5R5A1 \_ UNORM

-   DXGI \_ FORMAT \_ B8G8R8A8 \_ UNORM

-   DXGI \_ FORMAT \_ B8G8R8X8 \_ UNORM

Direct3D 版本 11 DDI 存在回退缓冲区限制。 如果设置了 dxgi 使用情况 \_ \_ 枚举 [ \_ ](/windows/win32/direct3ddxgi/dxgi-usage) 中的 dxgi 使用后台缓冲区 () 已设置，则只允许使用以下方法：

-   DXGI \_ 使用 \_ SHADERINPUT，它映射到 D3D11 \_ 绑定 \_ 着色器 \_ 资源

-   DXGI \_ 使用情况 \_ 呈现 \_ 目标 \_ 输出，映射到 D3D11 \_ 绑定 \_ 呈现器 \_ 目标

请注意，不允许对后台缓冲区使用任何 CPU 访问标志。

 

