---
title: 报告 DirectX 8.0 样式 Direct3D 功能
description: 报告 DirectX 8.0 样式 Direct3D 功能
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b04a0d899f2e23381fd651507c8f18e83111c8cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783963"
---
# <a name="reporting-directx-80-style-direct3d-capabilities"></a>报告 DirectX 8.0 样式 Direct3D 功能


## <span id="ddk_reporting_directx_8_0_style_direct3d_capabilities_gg"></span><span id="DDK_REPORTING_DIRECTX_8_0_STYLE_DIRECT3D_CAPABILITIES_GG"></span>


为了响应 D3DGDI2 类型 GETD3DCAPS8 类型的 **GetDriverInfo2** 查询 \_ \_ ，驱动程序应将已初始化的 D3DCAPS8 结构复制到 [**DD \_ lpvData**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)结构的 **GETDRIVERINFODATA** 字段。 此结构是 DirectX 8.0 的新增功能，并用于从驱动程序到运行时以及从运行时到应用程序的报告功能。

D3DCAPS8 提供了一些字段，这些字段介绍了 DirectX 8.0 的新增功能和从 DirectX 7.0 中的功能。 D3DCAPS8 不是现有功能的完整替换。 尽管此结构与受支持的图面格式的信息 () 是从 API 角度来看设备功能的完整说明，但并不适合于 DDI。 运行时使用驱动程序报告的 DirectDraw 功能作为支持的 surface 功能 (DDSCAPS) ，即使这些信息不是直接通过 DirectX 8.0 API 公开的。

此外，驱动程序还需要继续报告旧功能结构 (如使用旧接口的应用程序的 [**D3DHAL \_ D3DEXTENDEDCAPS**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps))  (DirectX 7.0 和更早版本) 继续请求这些功能。 因此，将 DirectX 8.0 style cap 通过 D3DCAPS8 报告是一种附加要求，而不是对现有功能报告机制的替代。 当应用程序使用 DirectX 8.0 接口时，运行时不会查询扩展 D3D 功能，如 D3DHAL \_ D3DEXTENDEDCAPS （如果驱动程序使用 D3DCAPS8 报告 DirectX 8.0 功能）。

DirectX 8.0 SDK 文档中介绍了 D3DCAPS8。 驱动程序不应初始化 **DeviceType** 或 **AdapterOrdinal** 字段。 运行时将这些值初始化为适当的值。 驱动程序应将这些字段设置为零。

 

