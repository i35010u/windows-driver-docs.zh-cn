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
ms.openlocfilehash: abce6988b654dd718214160ffa3dabd88a4f7e9c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063960"
---
# <a name="system-defined-ioctl_video_xxx-requests"></a>系统定义的 IOCTL \_ 视频 \_ XXX 请求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常，大多数视频微型端口驱动程序支持以下请求：

[**IOCTL \_ 视频 \_ 查询 \_ 的 \_ 可用 \_ 模式**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_num_avail_modes)

[**IOCTL \_ 视频 \_ 查询 \_ 可用 \_ 模式**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_avail_modes)

[**IOCTL \_ 视频 \_ 查询 \_ 当前 \_ 模式**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_current_mode)

[**IOCTL \_ 视频 \_ 设置 \_ 当前 \_ 模式**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)

[**IOCTL \_ 视频 \_ 重置 \_ 设备**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)

[**IOCTL \_ 视频 \_ 映射 \_ 视频 \_ 内存**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)

[**IOCTL \_ 视频取消 \_ 映射 \_ 视频 \_ 内存**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unmap_video_memory)

[**IOCTL \_ 视频 \_ 共享 \_ 视频 \_ 内存**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)

[**IOCTL \_ 视频取消 \_ 共享 \_ 视频 \_ 内存**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unshare_video_memory)

[**IOCTL \_ 视频 \_ 查询 \_ 公共 \_ 访问 \_ 范围**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_public_access_ranges)

[**IOCTL \_ 视频 \_ 免费 \_ 公共 \_ 访问 \_ 范围**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_free_public_access_ranges)

[**IOCTL \_ 视频 \_ 获取 \_ 电源 \_ 管理**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_power_management)

[**IOCTL \_ 视频 \_ 集 \_ 电源 \_ 管理**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_power_management)

[**IOCTL \_ 视频 \_ 获取 \_ 子 \_ 状态**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)

[**IOCTL \_ 视频 \_ 设置 \_ 子 \_ 状态 \_ 配置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_child_state_configuration)

[**IOCTL \_ 视频 \_ 验证 \_ 子 \_ 状态 \_ 配置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)

根据适配器的功能，视频微型端口驱动程序可以支持以下附加请求：

[**IOCTL \_ 视频 \_ 查询 \_ 颜色 \_ 功能**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)

[**IOCTL \_如果设备具有调色板，则视频 \_ 设置 \_ 颜色 \_ 寄存器**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_color_registers) (必需) 

[**IOCTL \_ 视频 \_ 禁用 \_ 指针**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_pointer)

[**IOCTL \_ 视频 \_ 启用 \_ 指针**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_pointer)

[**IOCTL \_ 视频 \_ 查询 \_ 指针 \_ 功能**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_capabilities)

[**IOCTL \_ 视频 \_ 查询 \_ 指针 \_ ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_attr)

[**IOCTL \_ 视频 \_ 集 \_ 指针 \_ ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_attr)

[**IOCTL \_ 视频 \_ 查询 \_ 指针 \_ 位置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_position)

[**IOCTL \_ 视频 \_ 集 \_ 指针 \_ 位置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_position)

[**IOCTL \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

[**IOCTL \_ 视频 \_ 开关 \_ 双屏**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)

需要 VGA 兼容的 SVGA 微型端口驱动程序来支持以下附加请求：

[**IOCTL \_ 视频 \_ 保存 \_ 硬件 \_ 状态**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_save_hardware_state)

[**IOCTL \_ 视频 \_ 还原 \_ 硬件 \_ 状态**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_restore_hardware_state)

[**IOCTL \_ 视频 \_ 禁用 \_ 光标**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_cursor)

[**IOCTL \_ 视频 \_ 启用 \_ 光标**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_cursor)

[**IOCTL \_ 视频 \_ 查询 \_ 游标 \_ ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_attr)

[**IOCTL \_ 视频 \_ 集 \_ CURSOR \_ ATTR**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_attr)

[**IOCTL \_ 视频 \_ 查询 \_ 游标 \_ 位置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_position)

[**IOCTL \_ 视频 \_ 设置 \_ 光标 \_ 位置**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_position)

[**IOCTL \_ 视频 \_ 获取 \_ 银行 \_ 选择 \_ 代码**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_bank_select_code)

[**IOCTL \_ 视频 \_ 集 \_ 调色板 \_ 寄存器**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_palette_registers)

[**IOCTL \_ 视频 \_ 加载 \_ 和 \_ 设置 \_ 字体**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_load_and_set_font)

有关每个 IOCTL 的详细信息，请参阅 [视频微型端口驱动程序 I/o 控制代码](/windows-hardware/drivers/ddi/index)。 微型端口驱动程序编写器不应使用未记录的系统定义的 IOCTLs。

 

