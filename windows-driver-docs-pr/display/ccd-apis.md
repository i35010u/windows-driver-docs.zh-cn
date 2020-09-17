---
title: CCD API
description: 连接和配置显示 (CCD) Api
ms.assetid: b71c1582-a91c-49d8-a3a3-d20f7746c354
keywords:
- 连接显示 WDK Windows 7 显示，CCD Api
- 连接显示 WDK Windows Server 2008 R2 显示，CCD Api
- 配置显示 WDK Windows 7 显示，CCD Api
- 配置显示 WDK Windows Server 2008 R2 显示，CCD Api
- CCD Api WDK Windows 7 显示
- CCD Api WDK Windows Server 2008 R2 显示
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3bb98b9f7214f36d01b1b5e82eab41799b205df0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715852"
---
# <a name="ccd-apis"></a>CCD API


此部分中的连接和配置显示 (CCD) Api 仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

## <a name="ccd-reference-for-user-mode-display-drivers"></a>用户模式显示驱动程序的 CCD 参考

本部分包含的参考页为连接和配置用户模式显示提供支持。 这些函数由用户模式显示驱动程序调用。


**CCD 函数**

**[DisplayConfigGetDeviceInfo](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo)**： [DisplayConfigSetDeviceInfo](/windows/win32/api/winuser/nf-winuser-displayconfigsetdeviceinfo)

**[GetDisplayConfigBufferSizes](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes)**： [QueryDisplayConfig](/windows/win32/api/winuser/nf-winuser-querydisplayconfig)

**[SetDisplayConfig](/windows/win32/api/winuser/nf-winuser-setdisplayconfig)**： 


 
**CCD 结构**

**[DISPLAYCONFIG_2DREGION](/windows/win32/api/wingdi/ns-wingdi-displayconfig_2dregion)**： [DISPLAYCONFIG_ADAPTER_NAME](/windows/win32/api/wingdi/ns-wingdi-displayconfig_adapter_name)

**[DISPLAYCONFIG_DEVICE_INFO_HEADER](/windows/win32/api/wingdi/ns-wingdi-displayconfig_device_info_header)**： [DISPLAYCONFIG_MODE_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_mode_info)

**[DISPLAYCONFIG_PATH_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_path_info)**： [DISPLAYCONFIG_PATH_SOURCE_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_path_source_info)

**[DISPLAYCONFIG_PATH_TARGET_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_path_target_info)**： [DISPLAYCONFIG_RATIONAL](/windows/win32/api/wingdi/ns-wingdi-displayconfig_rational)

**[DISPLAYCONFIG_SET_TARGET_PERSISTENCE](/windows/win32/api/wingdi/ns-wingdi-displayconfig_set_target_persistence)**： [DISPLAYCONFIG_SOURCE_DEVICE_NAME](/windows/win32/api/wingdi/ns-wingdi-displayconfig_source_device_name)

**[DISPLAYCONFIG_SOURCE_MODE](/windows/win32/api/wingdi/ns-wingdi-displayconfig_source_mode)**： [DISPLAYCONFIG_TARGET_DEVICE_NAME](/windows/win32/api/wingdi/ns-wingdi-displayconfig_target_device_name)

**[DISPLAYCONFIG_TARGET_DEVICE_NAME_FLAGS](/windows/win32/api/wingdi/ns-wingdi-displayconfig_target_device_name_flags)**： [DISPLAYCONFIG_TARGET_MODE](/windows/win32/api/wingdi/ns-wingdi-displayconfig_target_mode)

**[DISPLAYCONFIG_TARGET_PREFERRED_MODE](/windows/win32/api/wingdi/ns-wingdi-displayconfig_target_preferred_mode)**： [DISPLAYCONFIG_VIDEO_SIGNAL_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_video_signal_info)


 
**CCD 枚举**

**[DISPLAYCONFIG_DEVICE_INFO_TYPE](/windows/win32/api/wingdi/ne-wingdi-displayconfig_device_info_type)**： [DISPLAYCONFIG_MODE_INFO_TYPE](/windows/win32/api/wingdi/ne-wingdi-displayconfig_mode_info_type)

**[DISPLAYCONFIG_PIXELFORMAT](/windows/win32/api/wingdi/ne-wingdi-displayconfig_pixelformat)**： [DISPLAYCONFIG_ROTATION](/windows/win32/api/wingdi/ne-wingdi-displayconfig_rotation)

**[DISPLAYCONFIG_SCALING](/windows/win32/api/wingdi/ne-wingdi-displayconfig_scaling)**： [DISPLAYCONFIG_SCANLINE_ORDERING](/windows/win32/api/wingdi/ne-wingdi-displayconfig_scanline_ordering)

**[DISPLAYCONFIG_TOPOLOGY_ID](/windows/win32/api/wingdi/ne-wingdi-displayconfig_topology_id)**： [DISPLAYCONFIG_VIDEO_OUTPUT_TECHNOLOGY](/windows/win32/api/wingdi/ne-wingdi-displayconfig_video_output_technology)



以下部分介绍了 CCD Api，并演示了如何在一些示例代码中使用它们：

[CCD 摘要和方案](ccd-summaries-and-scenarios.md)

[CCD 示例代码](ccd-example-code.md)

 

