---
title: 系统定义的 IOCTL_VIDEO_XXX 请求
description: 系统定义的 IOCTL_VIDEO_XXX 请求
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，处理请求
- 请求处理 WDK 视频微型端口
- I/o WDK 视频微型端口
- 系统定义的 IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4843c05e503829155857805c1002f4308b5f22b1
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812521"
---
# <a name="system-defined-ioctl_video_xxx-requests"></a>系统定义的 IOCTL_VIDEO_XXX 请求

通常，大多数视频微型端口驱动程序支持以下请求：

[**IOCTL_VIDEO_QUERY_NUM_AVAIL_MODES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_num_avail_modes)

[**IOCTL_VIDEO_QUERY_AVAIL_MODES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_avail_modes)

[**IOCTL_VIDEO_QUERY_CURRENT_MODE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_current_mode)

[**IOCTL_VIDEO_SET_CURRENT_MODE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)

[**IOCTL_VIDEO_RESET_DEVICE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)

[**IOCTL_VIDEO_MAP_VIDEO_MEMORY**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)

[**IOCTL_VIDEO_UNMAP_VIDEO_MEMORY**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unmap_video_memory)

[**IOCTL_VIDEO_SHARE_VIDEO_MEMORY**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)

[**IOCTL_VIDEO_UNSHARE_VIDEO_MEMORY**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unshare_video_memory)

[**IOCTL_VIDEO_QUERY_PUBLIC_ACCESS_RANGES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_public_access_ranges)

[**IOCTL_VIDEO_FREE_PUBLIC_ACCESS_RANGES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_free_public_access_ranges)

[**IOCTL_VIDEO_GET_POWER_MANAGEMENT**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_power_management)

[**IOCTL_VIDEO_SET_POWER_MANAGEMENT**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_power_management)

[**IOCTL_VIDEO_GET_CHILD_STATE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)

[**IOCTL_VIDEO_SET_CHILD_STATE_CONFIGURATION**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_child_state_configuration)

[**IOCTL_VIDEO_VALIDATE_CHILD_STATE_CONFIGURATION**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)

根据适配器的功能，视频微型端口驱动程序可以支持以下附加请求：

[**IOCTL_VIDEO_QUERY_COLOR_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)

如果设备具有调色板，则 [**IOCTL_VIDEO_SET_COLOR_REGISTERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_color_registers) (必需) 

[**IOCTL_VIDEO_DISABLE_POINTER**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_pointer)

[**IOCTL_VIDEO_ENABLE_POINTER**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_pointer)

[**IOCTL_VIDEO_QUERY_POINTER_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_capabilities)

[**IOCTL_VIDEO_QUERY_POINTER_ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_attr)

[**IOCTL_VIDEO_SET_POINTER_ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_attr)

[**IOCTL_VIDEO_QUERY_POINTER_POSITION**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_position)

[**IOCTL_VIDEO_SET_POINTER_POSITION**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_position)

[**IOCTL_VIDEO_HANDLE_VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

[**IOCTL_VIDEO_SWITCH_DUALVIEW**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)

需要 VGA 兼容的 SVGA 微型端口驱动程序来支持以下附加请求：

[**IOCTL_VIDEO_SAVE_HARDWARE_STATE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_save_hardware_state)

[**IOCTL_VIDEO_RESTORE_HARDWARE_STATE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_restore_hardware_state)

[**IOCTL_VIDEO_DISABLE_CURSOR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_cursor)

[**IOCTL_VIDEO_ENABLE_CURSOR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_cursor)

[**IOCTL_VIDEO_QUERY_CURSOR_ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_attr)

[**IOCTL_VIDEO_SET_CURSOR_ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_attr)

[**IOCTL_VIDEO_QUERY_CURSOR_POSITION**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_position)

[**IOCTL_VIDEO_SET_CURSOR_POSITION**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_position)

[**IOCTL_VIDEO_GET_BANK_SELECT_CODE**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_bank_select_code)

[**IOCTL_VIDEO_SET_PALETTE_REGISTERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_palette_registers)

[**IOCTL_VIDEO_LOAD_AND_SET_FONT**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_load_and_set_font)

有关每个 IOCTL 的详细信息，请参阅 [视频微型端口驱动程序 I/o 控制代码](/windows-hardware/drivers/ddi/ntddvdeo)。 微型端口驱动程序编写器不应使用未记录的系统定义的 IOCTLs。
