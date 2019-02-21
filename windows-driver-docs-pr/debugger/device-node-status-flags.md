---
title: 设备节点状态标志
description: 设备节点状态标志
ms.assetid: 64f4548f-ace3-440c-8a36-97bd46cfa986
keywords:
- Plug and Play （即插即用），设备节点状态标志
- 设备节点状态标志
- DNF_XXX
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 256ad7a90f2bab282b98f16bb4f5e152e84aae98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555726"
---
# <a name="device-node-status-flags"></a>设备节点状态标志


## <span id="ddk_device_node_status_flags_dbg"></span><span id="DDK_DEVICE_NODE_STATUS_FLAGS_DBG"></span>


设备节点状态标志描述设备的状态。

最重要标志包括：

<span id="DNF_MADEUP__0x00000001_"></span><span id="dnf_madeup__0x00000001_"></span><span id="DNF_MADEUP__0X00000001_"></span>**DNF\_MADEUP (0x00000001)**  
已创建并拥有 PnP 管理器的设备。 它不被创建总线驱动程序。

<span id="DNF_DUPLICATE__0x00000002_"></span><span id="dnf_duplicate__0x00000002_"></span><span id="DNF_DUPLICATE__0X00000002_"></span>**DNF\_DUPLICATE (0x00000002)**  
设备节点是另一个枚举的设备节点的副本。

<span id="DNF_HAL_NODE__0x00000004_"></span><span id="dnf_hal_node__0x00000004_"></span><span id="DNF_HAL_NODE__0X00000004_"></span>**DNF\_HAL\_节点 (0x00000004)**  
设备节点是由硬件抽象层 (HAL) 创建的根节点。

<span id="DNF_REENUMERATE__0x00000008_"></span><span id="dnf_reenumerate__0x00000008_"></span><span id="DNF_REENUMERATE__0X00000008_"></span>**DNF\_REENUMERATE (0x00000008)**  
设备必须是重新枚举。

<span id="DNF_ENUMERATED__0x00000010_"></span><span id="dnf_enumerated__0x00000010_"></span><span id="DNF_ENUMERATED__0X00000010_"></span>**DNF\_ENUMERATED (0x00000010)**  
设备 PDO 被公开由其父级。

<span id="DNF_IDS_QUERIED__0x00000020_"></span><span id="dnf_ids_queried__0x00000020_"></span><span id="DNF_IDS_QUERIED__0X00000020_"></span>**DNF\_ID\_查询 (0x00000020)**  
操作系统应发送 IRP\_MN\_查询\_ID 请求设备驱动程序。

<span id="DNF_HAS_BOOT_CONFIG__0x00000040_"></span><span id="dnf_has_boot_config__0x00000040_"></span><span id="DNF_HAS_BOOT_CONFIG__0X00000040_"></span>**DNF\_HAS\_启动\_配置 (0x00000040)**  
该设备已由 BIOS 分配资源。 可将设备视为伪已启动，并且需要参与重新平衡。

<span id="DNF_BOOT_CONFIG_RESERVED__0x00000080_"></span><span id="dnf_boot_config_reserved__0x00000080_"></span><span id="DNF_BOOT_CONFIG_RESERVED__0X00000080_"></span>**DNF\_引导\_CONFIG\_保留 (0x00000080)**  
设备的启动资源被保留。

<span id="DNF_NO_RESOURCE_REQUIRED__0x00000100_"></span><span id="dnf_no_resource_required__0x00000100_"></span><span id="DNF_NO_RESOURCE_REQUIRED__0X00000100_"></span>**DNF\_否\_资源\_必需 (0x00000100)**  
设备不需要的资源。

<span id="DNF_RESOURCE_REQUIREMENTS_NEED_FILTERED__0x00000200_"></span><span id="dnf_resource_requirements_need_filtered__0x00000200_"></span><span id="DNF_RESOURCE_REQUIREMENTS_NEED_FILTERED__0X00000200_"></span>**DNF\_资源\_要求\_需要\_筛选 (0x00000200)**  
设备的资源要求列表是已筛选的列表。

<span id="DNF_RESOURCE_REQUIREMENTS_CHANGED__0x00000400_"></span><span id="dnf_resource_requirements_changed__0x00000400_"></span><span id="DNF_RESOURCE_REQUIREMENTS_CHANGED__0X00000400_"></span>**DNF\_资源\_要求\_CHANGED (0x00000400)**  
设备的资源要求列表已更改。

<span id="DNF_NON_STOPPED_REBALANCE__0x00000800_"></span><span id="dnf_non_stopped_rebalance__0x00000800_"></span><span id="DNF_NON_STOPPED_REBALANCE__0X00000800_"></span>**DNF\_非\_已停止\_重新平衡 (0x00000800)**  
设备可以使用新的资源未停止便已重新启动。

<span id="DNF_LEGACY_DRIVER__0x00001000_"></span><span id="dnf_legacy_driver__0x00001000_"></span><span id="DNF_LEGACY_DRIVER__0X00001000_"></span>**DNF\_LEGACY\_DRIVER (0x00001000)**  
设备的控制驱动程序是一个非 PnP 驱动程序。

<span id="DNF_HAS_PROBLEM__0x00002000_"></span><span id="dnf_has_problem__0x00002000_"></span><span id="DNF_HAS_PROBLEM__0X00002000_"></span>**DNF\_HAS\_问题 (0x00002000)**  
设备有问题，并将删除。

<span id="DNF_HAS_PRIVATE_PROBLEM__0x00004000_"></span><span id="dnf_has_private_problem__0x00004000_"></span><span id="DNF_HAS_PRIVATE_PROBLEM__0X00004000_"></span>**DNF\_HAS\_专用\_问题 (0x00004000)**  
设备报告 PNP\_设备\_失败，并且不会还报告 PNP\_设备\_资源\_要求\_已更改。

<span id="DNF_HARDWARE_VERIFICATION__0x00008000_"></span><span id="dnf_hardware_verification__0x00008000_"></span><span id="DNF_HARDWARE_VERIFICATION__0X00008000_"></span>**DNF\_硬件\_验证 (0x00008000)**  
设备节点都有硬件验证。

<span id="DNF_DEVICE_GONE__0x00010000_"></span><span id="dnf_device_gone__0x00010000_"></span><span id="DNF_DEVICE_GONE__0X00010000_"></span>**DNF\_DEVICE\_GONE (0x00010000)**  
在 IRP 中不再返回设备的 PDO\_查询\_关系请求。

<span id="DNF_LEGACY_RESOURCE_DEVICENODE__0x00020000_"></span><span id="dnf_legacy_resource_devicenode__0x00020000_"></span><span id="DNF_LEGACY_RESOURCE_DEVICENODE__0X00020000_"></span>**DNF\_旧版\_资源\_DEVICENODE (0x00020000)**  
设备节点是为旧的资源分配创建的。

<span id="DNF_NEEDS_REBALANCE__0x00040000_"></span><span id="dnf_needs_rebalance__0x00040000_"></span><span id="DNF_NEEDS_REBALANCE__0X00040000_"></span>**DNF\_NEEDS\_REBALANCE (0x00040000)**  
设备节点已触发重新均衡。

<span id="DNF_LOCKED_FOR_EJECT__0x00080000_"></span><span id="dnf_locked_for_eject__0x00080000_"></span><span id="DNF_LOCKED_FOR_EJECT__0X00080000_"></span>**DNF\_锁定\_为\_弹出 (0x00080000)**  
设备正在弹出或与正在弹出的设备相关。

<span id="DNF_DRIVER_BLOCKED__0x00100000_"></span><span id="dnf_driver_blocked__0x00100000_"></span><span id="DNF_DRIVER_BLOCKED__0X00100000_"></span>**DNF\_驱动程序\_已阻止 (0x00100000)**  
加载已阻止一个或多个设备节点的驱动程序。

<span id="DNF_CHILD_WITH_INVALID_ID__0x00200000_"></span><span id="dnf_child_with_invalid_id__0x00200000_"></span><span id="DNF_CHILD_WITH_INVALID_ID__0X00200000_"></span>**DNF\_子\_WITH\_无效\_ID (0x00200000)**  
设备节点的一个或多个子级具有无效的 Id。

<span id="DNF_ASYNC_START_NOT_SUPPORTED__0x00400000_"></span><span id="dnf_async_start_not_supported__0x00400000_"></span><span id="DNF_ASYNC_START_NOT_SUPPORTED__0X00400000_"></span>**DNF\_异步\_启动\_不\_支持 (0x00400000)**  
设备不支持异步启动。

<span id="DNF_ASYNC_ENUMERATION_NOT_SUPPORTED__0x00800000_"></span><span id="dnf_async_enumeration_not_supported__0x00800000_"></span><span id="DNF_ASYNC_ENUMERATION_NOT_SUPPORTED__0X00800000_"></span>**DNF\_异步\_枚举\_不\_支持 (0x00800000)**  
设备不支持异步枚举。

<span id="DNF_LOCKED_FOR_REBALANCE__0x01000000_"></span><span id="dnf_locked_for_rebalance__0x01000000_"></span><span id="DNF_LOCKED_FOR_REBALANCE__0X01000000_"></span>**DNF\_锁定\_为\_重新平衡 (0x01000000)**  
用于重新平衡锁定设备。

<span id="DNF_UNINSTALLED__0x02000000_"></span><span id="dnf_uninstalled__0x02000000_"></span><span id="DNF_UNINSTALLED__0X02000000_"></span>**DNF\_UNINSTALLED (0x02000000)**  
IRP\_MN\_查询\_删除\_设备请求正在进行的设备。

<span id="DNF_NO_LOWER_DEVICE_FILTERS__0x04000000_"></span><span id="dnf_no_lower_device_filters__0x04000000_"></span><span id="DNF_NO_LOWER_DEVICE_FILTERS__0X04000000_"></span>**DNF\_否\_较低\_设备\_筛选器 (0x04000000)**  
没有注册表项的较低设备筛选器类型的设备。

<span id="DNF_NO_LOWER_CLASS_FILTERS__0x08000000_"></span><span id="dnf_no_lower_class_filters__0x08000000_"></span><span id="DNF_NO_LOWER_CLASS_FILTERS__0X08000000_"></span>**DNF\_否\_较低\_类\_筛选器 (0x08000000)**  
没有注册表项的筛选器类较低的类型的设备。

<span id="DNF_NO_SERVICE__0x10000000_"></span><span id="dnf_no_service__0x10000000_"></span><span id="DNF_NO_SERVICE__0X10000000_"></span>**DNF\_否\_服务 (0x10000000)**  
该服务没有注册表条目的设备。

<span id="DNF_NO_UPPER_DEVICE_FILTERS__0x20000000_"></span><span id="dnf_no_upper_device_filters__0x20000000_"></span><span id="DNF_NO_UPPER_DEVICE_FILTERS__0X20000000_"></span>**DNF\_否\_上部\_设备\_筛选器 (0x20000000)**  
没有设备上限设备筛选器类型的注册表项。

<span id="DNF_NO_UPPER_CLASS_FILTERS__0x40000000_"></span><span id="dnf_no_upper_class_filters__0x40000000_"></span><span id="DNF_NO_UPPER_CLASS_FILTERS__0X40000000_"></span>**DNF\_否\_上部\_类\_筛选器 (0x40000000)**  
没有上限类筛选类型设备的注册表项。

<span id="DNF_WAITING_FOR_FDO__0x80000000_"></span><span id="dnf_waiting_for_fdo__0x80000000_"></span><span id="DNF_WAITING_FOR_FDO__0X80000000_"></span>**DNF\_等待\_为\_FDO (0x80000000)**  
枚举的设备正在等待，直到驱动程序将附加其 FDO。

 

 





