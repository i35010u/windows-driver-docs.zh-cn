---
title: Direct3D 版本 9 驱动程序的 DDI 更改
description: Direct3D 版本 9 驱动程序的 DDI 更改
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示、Direct3D 版本9驱动程序的 DDI 更改
- Direct3D 版本9驱动程序 WDK Windows 7 显示
- Direct3D 版本9驱动程序 WDK Windows 7 显示，DDI 更改
- XR_BIAS WDK Windows 7 显示，Direct3D 版本 9 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe6e4f561b3930962d84c7431c91e07dfad9d3de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820839"
---
# <a name="ddi-changes-for-direct3d-version-9-drivers"></a>Direct3D 版本 9 驱动程序的 DDI 更改


本部分仅适用于 Windows 7 及更高版本的操作系统。

XR \_ 偏向是 Windows 7 为仅支持 Direct3D 版本 9 DDI 的用户模式显示驱动程序提供的新扩展格式功能。

此类用户模式显示驱动程序可以指示它支持 \_ \_ D3DDDIFORMAT 枚举中的 D3DDDIFMT A2B10G10R10 XR \_ 偏向格式值 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat) 。 该驱动程序通过在 D3DDDIARG GETCAPS 结构的 PData 成员的 [**FORMATOP**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)结构的数组中创建一个条目来指出此类支持，驱动程序将在 [**\_**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的 **pData** 成员中通过调用 [**GETCAPS 函数并**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)在 \_ D3DDDICAPS **Type** \_ GETFORMATDATA 此项应在 **FORMATOP** 的 **操作** 成员中指出，运行时可以在具有 D3DDDIFMT \_ A2B10G10R10 \_ XR 偏向格式的表面上执行的所有典型操作 \_ 。 例如，驱动程序应 \_ \* \_ 在 **操作** 中设置 FORMATOP RENDERTARGET 位。 驱动程序还必须 \_ 在操作中设置 FORMATOP DISPLAYMODE 和 FORMATOP \_ 3DACCELERATION **Operations** 位。

如果驱动程序为 D3DDDIFMT [**FORMATOP**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop) \_ A2B10G10R10 \_ XR 偏向格式返回 FORMATOP 项 \_ ，则驱动程序随后可以接收对其 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数的调用，以在 \_ D3DDDIFMT A2B10G10R10 结构的 \_ \_ **format** 成员中使用 XR D3DDDIARG CreateResource 偏向格式集 [**\_**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)创建资源。

驱动程序仅接收为全屏翻转链创建具有 D3DDDIFMT \_ A2B10G10R10 \_ XR 偏向格式的资源的请求 \_ 。 桌面 Windows 管理器 (DWM) 处理 \_ 着色器代码中的 XR 偏移的窗口化表示形式。 驱动程序应将 D3DDDIFMT \_ A2B10G10R10 \_ XR \_ 偏向格式的资源视为 \_ 除扫描之外的所有操作中的 D3DDDIFMT A2B10G10R10 格式，例如，驱动程序可以将 D3DDDIFMT \_ A2B10G10R10 \_ XR \_ 偏向格式的资源视为 \_ 用于混合、筛选和格式转换操作的 D3DDDIFMT A2B10G10R10 格式。 唯一的区别是 XR \_ 偏向如何影响扫描。有关扫描的详细信息，请参阅 [BGRA Scan-Out 支持](bgra-scan-out-support.md)。

 

