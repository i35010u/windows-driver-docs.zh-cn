---
title: 报告 DirectX 8.0 样式 Direct3D 功能
description: 报告 DirectX 8.0 样式 Direct3D 功能
ms.assetid: a03a7cbc-95be-4251-8e3a-bef4a093f03d
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb0125cb026266a5f85b3d37cb477e1ad696386
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825941"
---
# <a name="reporting-directx-80-style-direct3d-capabilities"></a>报告 DirectX 8.0 样式 Direct3D 功能


## <span id="ddk_reporting_directx_8_0_style_direct3d_capabilities_gg"></span><span id="DDK_REPORTING_DIRECTX_8_0_STYLE_DIRECT3D_CAPABILITIES_GG"></span>


为了响应类型为 D3DGDI2\_类型为\_GETD3DCAPS8 的**GetDriverInfo2**查询，驱动程序应将已初始化 D3DCAPS8 结构复制到[**DD\_LpvData**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构的**GETDRIVERINFODATA**字段。 此结构是 DirectX 8.0 的新增功能，并用于从驱动程序到运行时以及从运行时到应用程序的报告功能。

D3DCAPS8 提供了一些字段，这些字段介绍了 DirectX 8.0 的新增功能和从 DirectX 7.0 中的功能。 D3DCAPS8 不是现有功能的完整替换。 尽管此结构（以及受支持的表面格式的信息）是从 API 角度来看设备功能的完整说明，但对于 DDI 而言，这并不是足够的。 运行时使用驱动程序报告的 DirectDraw 功能作为支持的 surface 功能（DDSCAPS）的信息，即使这些信息不是直接通过 DirectX 8.0 API 公开的。

此外，如果应用程序使用旧接口（DirectX 7.0 及更早版本），则需要使用驱动程序继续报告旧功能结构（如[**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)），以继续请求这些功能。 因此，将 DirectX 8.0 style cap 通过 D3DCAPS8 报告是一种附加要求，而不是对现有功能报告机制的替代。 当应用程序使用 DirectX 8.0 接口时，如果驱动程序使用 D3DCAPS8 报告 DirectX 8.0 功能，则运行时不会查询扩展 D3D 功能，如 D3DHAL\_D3DEXTENDEDCAPS。

DirectX 8.0 SDK 文档中介绍了 D3DCAPS8。 驱动程序不应初始化**DeviceType**或**AdapterOrdinal**字段。 运行时将这些值初始化为适当的值。 驱动程序应将这些字段设置为零。

 

 





