---
title: 系统定义的 IOCTL_VIDEO_XXX 请求
description: 系统定义的 IOCTL_VIDEO_XXX 请求
ms.assetid: 30309de1-c991-402d-a701-7e88c3367d24
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，处理请求
- 请求处理 WDK 视频微型端口
- I/o WDK 视频微型端口
- 系统定义的 IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33bb4fe9a28878c97099c2a6bcf123f569c6097f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825509"
---
# <a name="system-defined-ioctl_video_xxx-requests"></a>系统定义的 IOCTL\_视频\_XXX 请求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常，大多数视频微型端口驱动程序支持以下请求：

[**IOCTL\_视频\_QUERY\_\_可用\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_num_avail_modes)

[ **\_可用\_模式的 IOCTL\_视频\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_avail_modes)

[**IOCTL\_视频\_QUERY\_当前\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_current_mode)

[ **\_视频\_设置\_当前\_模式的 IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)

[**IOCTL\_视频\_重置\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)

[**IOCTL\_视频\_地图\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)

[**IOCTL\_视频\_取消\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unmap_video_memory)

[**IOCTL\_视频\_共享\_视频\_内存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)

[**IOCTL\_视频\_取消\_视频\_内存的共享**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unshare_video_memory)

[**IOCTL\_视频\_查询\_公共\_ACCESS\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_public_access_ranges)

[**IOCTL\_视频\_免费\_公共\_ACCESS\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_free_public_access_ranges)

[**IOCTL\_视频\_获取\_电源\_管理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_power_management)

[**IOCTL\_视频\_集\_电源\_管理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_power_management)

[**IOCTL\_视频\_获取\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)

[**IOCTL\_视频\_设置\_子\_状态\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_child_state_configuration)

[**IOCTL\_视频\_验证\_子\_状态\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)

根据适配器的功能，视频微型端口驱动程序可以支持以下附加请求：

[**IOCTL\_视频\_查询\_颜色\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)

[**IOCTL\_视频\_设置\_颜色\_寄存器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_color_registers)（设备具有调色板时需要）

[**IOCTL\_视频\_禁用\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_pointer)

[**IOCTL\_视频\_启用\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_pointer)

[**IOCTL\_视频\_查询\_指针\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_capabilities)

[**IOCTL\_视频\_查询\_指针\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_attr)

[**IOCTL\_视频\_设置\_指针\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_attr)

[**IOCTL\_视频\_查询\_指针\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_position)

[**IOCTL\_视频\_设置\_指针\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_position)

[**IOCTL\_视频\_句柄\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

[**IOCTL\_视频\_开关\_双屏**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)

需要 VGA 兼容的 SVGA 微型端口驱动程序来支持以下附加请求：

[**IOCTL\_视频\_保存\_硬件\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_save_hardware_state)

[**IOCTL\_视频\_还原\_硬件\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_restore_hardware_state)

[**IOCTL\_视频\_禁用\_光标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_cursor)

[**IOCTL\_视频\_启用\_光标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_cursor)

[**IOCTL\_视频\_QUERY\_CURSOR\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_attr)

[**IOCTL\_视频\_设置\_CURSOR\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_attr)

[**IOCTL\_视频\_查询\_光标\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_position)

[**IOCTL\_视频\_集\_光标\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_position)

[**IOCTL\_视频\_获取\_银行\_选择\_代码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_bank_select_code)

[**IOCTL\_视频\_集\_寄存器\_组件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_palette_registers)

[**IOCTL\_视频\_负载\_和\_设置\_字体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_load_and_set_font)

有关每个 IOCTL 的详细信息，请参阅[视频微型端口驱动程序 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 微型端口驱动程序编写器不应使用未记录的系统定义的 IOCTLs。

 

 





