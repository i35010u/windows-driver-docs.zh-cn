---
title: 报告 DirectX 8.0 样式 Direct3D 功能
description: 报告 DirectX 8.0 样式 Direct3D 功能
ms.assetid: a03a7cbc-95be-4251-8e3a-bef4a093f03d
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb0be0d01506d78f4ff97483d6a485d651862434
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383273"
---
# <a name="reporting-directx-80-style-direct3d-capabilities"></a>报告 DirectX 8.0 样式 Direct3D 功能


## <span id="ddk_reporting_directx_8_0_style_direct3d_capabilities_gg"></span><span id="DDK_REPORTING_DIRECTX_8_0_STYLE_DIRECT3D_CAPABILITIES_GG"></span>


以响应**GetDriverInfo2**查询与类型 D3DGDI2\_类型\_GETD3DCAPS8，驱动程序应将复制到一个初始化的 D3DCAPS8 结构**lpvData**字段[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构。 此结构是 DirectX 8.0 的新增功能，用于从驱动程序添加到运行时和应用程序的运行时这两个报告功能。

D3DCAPS8 具有描述这两个功能对 DirectX 8.0 的新的字段并且功能执行 DirectX 7.0 从转发。 D3DCAPS8 不是完全取代现有功能。 尽管此结构 （以及受支持的图面上格式的信息） API 的角度看来自设备的功能的完整说明，但它是不够的 DDI。 在运行时利用了 DirectDraw 功能报告的此类信息作为该驱动程序支持的图面上的功能 (DDSCAPS) 即使这些不会直接通过 DirectX 8.0 API 公开。

此外，驱动程序才能继续对报表旧功能结构 (如[ **D3DHAL\_D3DEXTENDEDCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff544753)) 作为使用旧式界面的应用程序 (DirectX 7.0 和之前的版本） 继续请求这些功能。 因此，报告通过 D3DCAPS8 DirectX 8.0 样式 cap 是一个额外的要求，而不是替换现有的功能报告机制。 DirectX 8.0 接口用于时由运行时不会查询应用程序扩展的 D3D 功能，例如 D3DHAL\_D3DEXTENDEDCAPS 如果驱动程序报告了 D3DCAPS8 DirectX 8.0 功能。

D3DCAPS8 是 DirectX 8.0 SDK 文档中所述。 该驱动程序应初始化**DeviceType**或**AdapterOrdinal**字段。 这些是由运行时初始化为适当的值。 该驱动程序应将这些字段设置为零。

 

 





