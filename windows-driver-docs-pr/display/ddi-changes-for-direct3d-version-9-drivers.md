---
title: Direct3D 版本 9 驱动程序的 DDI 更改
description: Direct3D 版本 9 驱动程序的 DDI 更改
ms.assetid: b702c02d-3be6-46e8-9e53-5d33e5e3fc70
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示、Direct3D 版本9驱动程序的 DDI 更改
- Direct3D 版本9驱动程序 WDK Windows 7 显示
- Direct3D 版本9驱动程序 WDK Windows 7 显示，DDI 更改
- XR_BIAS WDK Windows 7 显示，Direct3D 版本 9 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7433326539dd5e9da3ff2022b61d91bb371f31d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839020"
---
# <a name="ddi-changes-for-direct3d-version-9-drivers"></a>Direct3D 版本 9 驱动程序的 DDI 更改


本部分仅适用于 Windows 7 及更高版本的操作系统。

XR\_偏向是 Windows 7 向仅支持 Direct3D 版本 9 DDI 的用户模式显示驱动程序提供的新扩展格式功能。

此类用户模式显示驱动程序可以指示它支持[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举中的 D3DDDIFMT\_A2B10G10R10\_XR\_偏向格式值。 该驱动程序通过在[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps) [**结构的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop) **pData**成员中创建一个条目，在此类支持中创建一个条目，驱动程序将使用 GETCAPS\_D3DDDICAPS 值（在 GETFORMATDATA\_D3DDDIARG 的**类型**成员中设置）调用[**GETCAPS 函数。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps) 此项应在**FORMATOP**的**操作**成员中指出，运行时可以在具有 D3DDDIFMT\_A2B10G10R10\_XR\_偏向格式的表面上执行的所有典型操作。 例如，驱动程序应设置**操作**中\*\_的 FORMATOP\_。 驱动程序还必须在**操作**中设置 FORMATOP\_DISPLAYMODE 和 FORMATOP\_3DACCELERATION 位。

如果驱动程序返回 D3DDDIFMT\_A2B10G10R10\_XR\_偏向格式的[**FORMATOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)项，则驱动程序可以随后接收对其[**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数的调用，以使用 D3DDDIFMT 创建资源\_A2B10G10R10\_XR\_在[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**格式**成员中设置的偏移量格式。

驱动程序只接收到用 D3DDDIFMT\_A2B10G10R10\_XR\_偏向格式为全屏翻转链创建资源的请求。 桌面窗口管理器（DWM）处理着色器代码中的 XR\_偏差的窗口化表示形式。 驱动程序应将 D3DDDIFMT\_A2B10G10R10\_XR\_偏向格式的资源视为除扫描之外的所有操作中的 D3DDDIFMT\_A2B10G10R10 格式，例如，驱动程序可以将 D3DDDIFMT 视为 A2B10G10R10\_XR\_偏向格式的资源，作为用于混合、筛选和格式转换操作的 D3DDDIFMT\_A2B10G10R10 格式。\_ 唯一的区别是 XR\_偏向如何影响扫描。有关扫描的详细信息，请参阅[BGRA 扫描支持](bgra-scan-out-support.md)。

 

 





