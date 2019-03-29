---
title: CCD API
description: 连接和配置 Api (CCD) 显示
ms.assetid: b71c1582-a91c-49d8-a3a3-d20f7746c354
keywords:
- 连接显示 WDK Windows 7 显示 CCD Api
- 连接显示 WDK Windows Server 2008 R2 显示 CCD Api
- 配置显示 WDK Windows 7 显示 CCD Api
- 配置显示 WDK Windows Server 2008 R2 显示 CCD Api
- CCD Api WDK Windows 7 显示
- CCD Api WDK Windows Server 2008 R2 显示
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4561188374d6a18afd66a5b71240367f29f2458a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576355"
---
# <a name="ccd-apis"></a>CCD API


连接和配置显示在本部分中的 (CCD) Api 仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

## <a name="ccd-reference-for-user-mode-display-drivers"></a>CCD 用户模式显示驱动程序的引用

本部分包含用于连接提供支持的参考页并配置用户模式下显示。 用户模式显示驱动程序调用函数时。


**CCD 函数**

|||
|:--|:--|
|[DisplayConfigGetDeviceInfo](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)|[DisplayConfigSetDeviceInfo](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)|
|[GetDisplayConfigBufferSizes](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)|[QueryDisplayConfig](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)|
|[SetDisplayConfig](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)||

 
**CCD 结构**

|||
|:--|:--|
|[DISPLAYCONFIG_2DREGION](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_2dregion)|[DISPLAYCONFIG_ADAPTER_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_adapter_name)|
|[DISPLAYCONFIG_DEVICE_INFO_HEADER](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_device_info_header)|[DISPLAYCONFIG_MODE_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_mode_info)|
|[DISPLAYCONFIG_PATH_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_info)|[DISPLAYCONFIG_PATH_SOURCE_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_source_info)|
|[DISPLAYCONFIG_PATH_TARGET_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_path_target_info)|[DISPLAYCONFIG_RATIONAL](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_rational)|
|[DISPLAYCONFIG_SET_TARGET_PERSISTENCE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_set_target_persistence)|[DISPLAYCONFIG_SOURCE_DEVICE_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_device_name)|
|[DISPLAYCONFIG_SOURCE_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_mode)|[DISPLAYCONFIG_TARGET_DEVICE_NAME](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_device_name)|
|[DISPLAYCONFIG_TARGET_DEVICE_NAME_FLAGS](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_device_name_flags)|[DISPLAYCONFIG_TARGET_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_mode)|
|[DISPLAYCONFIG_TARGET_PREFERRED_MODE](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_preferred_mode)|[DISPLAYCONFIG_VIDEO_SIGNAL_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)|

 
**CCD 枚举**

|||
|:--|:--|
|[DISPLAYCONFIG_DEVICE_INFO_TYPE](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type)|[DISPLAYCONFIG_MODE_INFO_TYPE](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_mode_info_type)|
|[DISPLAYCONFIG_PIXELFORMAT](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_pixelformat)|[DISPLAYCONFIG_ROTATION](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_rotation)|
|[DISPLAYCONFIG_SCALING](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_scaling)|[DISPLAYCONFIG_SCANLINE_ORDERING](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_scanline_ordering)|
|[DISPLAYCONFIG_TOPOLOGY_ID](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_topology_id)|[DISPLAYCONFIG_VIDEO_OUTPUT_TECHNOLOGY](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)|


以下各节描述 CCD Api 并演示如何在一些示例代码中使用它们：

[CCD 摘要和方案](ccd-summaries-and-scenarios.md)

[CCD 示例代码](ccd-example-code.md)

 

 





