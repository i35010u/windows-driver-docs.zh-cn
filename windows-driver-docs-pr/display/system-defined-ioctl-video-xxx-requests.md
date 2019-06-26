---
title: 系统定义的 IOCTL_VIDEO_XXX 请求
description: 系统定义的 IOCTL_VIDEO_XXX 请求
ms.assetid: 30309de1-c991-402d-a701-7e88c3367d24
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，处理请求
- 请求处理 WDK 微型端口
- I/O WDK 微型端口
- 系统定义 IOCTL_VIDEO_XXX 请求 WDK 微型端口
- IOCTL_VIDEO_XXX 请求 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6079c34645379d4a052b24faad76a28b6c7904b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372052"
---
# <a name="system-defined-ioctlvideoxxx-requests"></a>系统定义 IOCTL\_视频\_XXX 请求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常情况下，大多数微型端口驱动程序支持以下请求：

[**IOCTL\_视频\_查询\_NUM\_利用\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_num_avail_modes)

[**IOCTL\_视频\_查询\_利用\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_avail_modes)

[**IOCTL\_视频\_查询\_当前\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_current_mode)

[**IOCTL\_视频\_设置\_当前\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)

[**IOCTL\_VIDEO\_RESET\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)

[**IOCTL\_视频\_地图\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)

[**IOCTL\_视频\_UNMAP\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_unmap_video_memory)

[**IOCTL\_视频\_共享\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)

[**IOCTL\_视频\_取消共享\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_unshare_video_memory)

[**IOCTL\_视频\_查询\_公共\_访问\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_public_access_ranges)

[**IOCTL\_视频\_免费\_公共\_访问\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_free_public_access_ranges)

[**IOCTL\_视频\_获取\_POWER\_管理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_power_management)

[**IOCTL\_VIDEO\_SET\_POWER\_MANAGEMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_power_management)

[**IOCTL\_VIDEO\_GET\_CHILD\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)

[**IOCTL\_VIDEO\_SET\_CHILD\_STATE\_CONFIGURATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_child_state_configuration)

[**IOCTL\_视频\_VALIDATE\_子\_状态\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)

具体取决于适配器的功能，微型端口驱动程序可以支持以下额外的请求：

[**IOCTL\_视频\_查询\_颜色\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)

[**IOCTL\_视频\_设置\_颜色\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_color_registers) （如果设备具有调色板为必需）

[**IOCTL\_视频\_禁用\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_pointer)

[**IOCTL\_VIDEO\_ENABLE\_POINTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_pointer)

[**IOCTL\_视频\_查询\_指针\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_capabilities)

[**IOCTL\_视频\_查询\_指针\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_attr)

[**IOCTL\_VIDEO\_SET\_POINTER\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_attr)

[**IOCTL\_视频\_查询\_指针\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_position)

[**IOCTL\_视频\_设置\_指针\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_position)

[**IOCTL\_VIDEO\_HANDLE\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

[**IOCTL\_视频\_交换机\_双视图**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)

支持以下其他请求所需的 VGA 兼容的 SVGA 微型端口驱动程序：

[**IOCTL\_VIDEO\_SAVE\_HARDWARE\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_save_hardware_state)

[**IOCTL\_视频\_还原\_硬件\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_restore_hardware_state)

[**IOCTL\_视频\_禁用\_游标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_cursor)

[**IOCTL\_视频\_启用\_游标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_cursor)

[**IOCTL\_视频\_查询\_光标\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_attr)

[**IOCTL\_视频\_设置\_光标\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_attr)

[**IOCTL\_视频\_查询\_光标\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_position)

[**IOCTL\_视频\_设置\_光标\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_position)

[**IOCTL\_VIDEO\_GET\_BANK\_SELECT\_CODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_bank_select_code)

[**IOCTL\_视频\_设置\_调色板\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_palette_registers)

[**IOCTL\_视频\_负载\_AND\_设置\_字体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_load_and_set_font)

可以在找到每个 IOCTL 详细信息[视频微型端口驱动程序 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 微型端口驱动程序编写人员不应使用未记录的系统定义 Ioctl。

 

 





