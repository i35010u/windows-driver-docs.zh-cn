---
title: 设备节点状态标志
description: 设备节点状态标志
keywords:
- 即插即用 (PnP) ，设备节点状态标志
- 设备节点状态标志
- DNF_XXX
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5940547511e1e2c63b01698657d8bc16976f6263
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818637"
---
# <a name="device-node-status-flags"></a>设备节点状态标志


## <span id="ddk_device_node_status_flags_dbg"></span><span id="DDK_DEVICE_NODE_STATUS_FLAGS_DBG"></span>


设备节点状态标志描述设备的状态。

最重要的标志是：

<span id="DNF_MADEUP__0x00000001_"></span><span id="dnf_madeup__0x00000001_"></span><span id="DNF_MADEUP__0X00000001_"></span>**DNF \_ MADEUP (0x00000001)**  
设备已创建，并由 PnP 管理器拥有。 它不是由总线驱动程序创建的。

<span id="DNF_DUPLICATE__0x00000002_"></span><span id="dnf_duplicate__0x00000002_"></span><span id="DNF_DUPLICATE__0X00000002_"></span>**DNF \_ 重复 (0x00000002)**  
设备节点是另一个枚举设备节点的副本。

<span id="DNF_HAL_NODE__0x00000004_"></span><span id="dnf_hal_node__0x00000004_"></span><span id="DNF_HAL_NODE__0X00000004_"></span>**DNF \_ HAL \_ 节点 (0x00000004)**  
设备节点是由硬件抽象层 (HAL) 创建的根节点。

<span id="DNF_REENUMERATE__0x00000008_"></span><span id="dnf_reenumerate__0x00000008_"></span><span id="DNF_REENUMERATE__0X00000008_"></span>**DNF \_ REENUMERATE (0x00000008)**  
需要重新枚举设备。

<span id="DNF_ENUMERATED__0x00000010_"></span><span id="dnf_enumerated__0x00000010_"></span><span id="DNF_ENUMERATED__0X00000010_"></span>**DNF \_ 枚举 (0x00000010)**  
设备的 PDO 由其父项公开。

<span id="DNF_IDS_QUERIED__0x00000020_"></span><span id="dnf_ids_queried__0x00000020_"></span><span id="DNF_IDS_QUERIED__0X00000020_"></span>**\_ \_ (0x00000020) 查询的 DNF id**  
操作系统应将 IRP \_ MN \_ 查询 \_ ID 请求发送到设备驱动程序。

<span id="DNF_HAS_BOOT_CONFIG__0x00000040_"></span><span id="dnf_has_boot_config__0x00000040_"></span><span id="DNF_HAS_BOOT_CONFIG__0X00000040_"></span>**DNF \_ 具有 \_ BOOT \_ CONFIG (0x00000040)**  
设备包含 BIOS 分配的资源。 设备被视为伪启动的设备，需要参与重新平衡。

<span id="DNF_BOOT_CONFIG_RESERVED__0x00000080_"></span><span id="dnf_boot_config_reserved__0x00000080_"></span><span id="DNF_BOOT_CONFIG_RESERVED__0X00000080_"></span>**DNF \_ BOOT \_ CONFIG \_ RESERVED (0x00000080)**  
设备的启动资源是保留的。

<span id="DNF_NO_RESOURCE_REQUIRED__0x00000100_"></span><span id="dnf_no_resource_required__0x00000100_"></span><span id="DNF_NO_RESOURCE_REQUIRED__0X00000100_"></span>**DNF \_ 无 \_ \_ 需资源 (0x00000100)**  
设备不需要资源。

<span id="DNF_RESOURCE_REQUIREMENTS_NEED_FILTERED__0x00000200_"></span><span id="dnf_resource_requirements_need_filtered__0x00000200_"></span><span id="DNF_RESOURCE_REQUIREMENTS_NEED_FILTERED__0X00000200_"></span>**DNF \_ 资源 \_ 需求 \_ 需要 \_ 筛选 (0x00000200)**  
设备的资源要求列表是筛选后的列表。

<span id="DNF_RESOURCE_REQUIREMENTS_CHANGED__0x00000400_"></span><span id="dnf_resource_requirements_changed__0x00000400_"></span><span id="DNF_RESOURCE_REQUIREMENTS_CHANGED__0X00000400_"></span>**DNF \_ 资源 \_ 需求 \_ 更改 (0x00000400)**  
设备的资源需求列表已更改。

<span id="DNF_NON_STOPPED_REBALANCE__0x00000800_"></span><span id="dnf_non_stopped_rebalance__0x00000800_"></span><span id="DNF_NON_STOPPED_REBALANCE__0X00000800_"></span>**DNF \_ 未 \_ 停止的重新 \_ 平衡 (0x00000800)**  
可以通过新的资源重新启动设备，而无需停止。

<span id="DNF_LEGACY_DRIVER__0x00001000_"></span><span id="dnf_legacy_driver__0x00001000_"></span><span id="DNF_LEGACY_DRIVER__0X00001000_"></span>**DNF \_ 传统 \_ 驱动程序 (0x00001000)**  
设备的控制驱动程序是非 PnP 驱动程序。

<span id="DNF_HAS_PROBLEM__0x00002000_"></span><span id="dnf_has_problem__0x00002000_"></span><span id="DNF_HAS_PROBLEM__0X00002000_"></span>**DNF \_ \_)  (的问题**  
设备有问题，将被删除。

<span id="DNF_HAS_PRIVATE_PROBLEM__0x00004000_"></span><span id="dnf_has_private_problem__0x00004000_"></span><span id="DNF_HAS_PRIVATE_PROBLEM__0X00004000_"></span>**DNF \_ \_ \_)  (的隐私问题**  
设备报告 PNP \_ 设备 \_ 失败，同时未报告 pnp \_ 设备 \_ 资源 \_ 要求 \_ 已更改。

<span id="DNF_HARDWARE_VERIFICATION__0x00008000_"></span><span id="dnf_hardware_verification__0x00008000_"></span><span id="DNF_HARDWARE_VERIFICATION__0X00008000_"></span>**DNF \_ 硬件 \_ 验证 (0x00008000)**  
设备节点具有硬件验证。

<span id="DNF_DEVICE_GONE__0x00010000_"></span><span id="dnf_device_gone__0x00010000_"></span><span id="DNF_DEVICE_GONE__0X00010000_"></span>**DNF \_ 设备 \_ 消失 (0x00010000)**  
IRP \_ 查询关系请求中不再返回设备的 PDO \_ 。

<span id="DNF_LEGACY_RESOURCE_DEVICENODE__0x00020000_"></span><span id="dnf_legacy_resource_devicenode__0x00020000_"></span><span id="DNF_LEGACY_RESOURCE_DEVICENODE__0X00020000_"></span>**DNF \_ 传统 \_ 资源 \_ DEVICENODE (0x00020000)**  
已为旧资源分配创建设备节点。

<span id="DNF_NEEDS_REBALANCE__0x00040000_"></span><span id="dnf_needs_rebalance__0x00040000_"></span><span id="DNF_NEEDS_REBALANCE__0X00040000_"></span>**DNF \_ 需要重新 \_ 平衡 (0x00040000)**  
设备节点触发了重新平衡。

<span id="DNF_LOCKED_FOR_EJECT__0x00080000_"></span><span id="dnf_locked_for_eject__0x00080000_"></span><span id="DNF_LOCKED_FOR_EJECT__0X00080000_"></span>**DNF \_ 锁定 \_ ， \_ 弹出 (0x00080000)**  
设备正在弹出，或与要弹出的设备相关。

<span id="DNF_DRIVER_BLOCKED__0x00100000_"></span><span id="dnf_driver_blocked__0x00100000_"></span><span id="DNF_DRIVER_BLOCKED__0X00100000_"></span>**DNF \_ 驱动程序已 \_ 阻止 (0x00100000)**  
设备节点的一个或多个驱动程序已被阻止加载。

<span id="DNF_CHILD_WITH_INVALID_ID__0x00200000_"></span><span id="dnf_child_with_invalid_id__0x00200000_"></span><span id="DNF_CHILD_WITH_INVALID_ID__0X00200000_"></span>**\_ \_ \_ \_ ID (0x00200000) 的 DNF 子元素**  
设备节点的一个或多个子项具有无效的 Id。

<span id="DNF_ASYNC_START_NOT_SUPPORTED__0x00400000_"></span><span id="dnf_async_start_not_supported__0x00400000_"></span><span id="DNF_ASYNC_START_NOT_SUPPORTED__0X00400000_"></span>**\_ \_ 不支持 DNF 异步启动 \_ \_ (0x00400000)**  
设备不支持异步启动。

<span id="DNF_ASYNC_ENUMERATION_NOT_SUPPORTED__0x00800000_"></span><span id="dnf_async_enumeration_not_supported__0x00800000_"></span><span id="DNF_ASYNC_ENUMERATION_NOT_SUPPORTED__0X00800000_"></span>**\_ \_ 不支持 DNF 异步枚举 \_ \_ (0x00800000)**  
设备不支持异步枚举。

<span id="DNF_LOCKED_FOR_REBALANCE__0x01000000_"></span><span id="dnf_locked_for_rebalance__0x01000000_"></span><span id="DNF_LOCKED_FOR_REBALANCE__0X01000000_"></span>**DNF \_ 锁定 \_ \_ (0x01000000)**  
设备已锁定，无法重新平衡。

<span id="DNF_UNINSTALLED__0x02000000_"></span><span id="dnf_uninstalled__0x02000000_"></span><span id="DNF_UNINSTALLED__0X02000000_"></span>**DNF \_ 卸载 (0x02000000)**  
正在 \_ 为设备执行 IRP MN \_ 查询 \_ 删除 \_ 设备请求。

<span id="DNF_NO_LOWER_DEVICE_FILTERS__0x04000000_"></span><span id="dnf_no_lower_device_filters__0x04000000_"></span><span id="DNF_NO_LOWER_DEVICE_FILTERS__0X04000000_"></span>**DNF \_ \_ \_ \_)  (的设备筛选器不低于0x04000000**  
设备的设备筛选器类型的注册表项不存在。

<span id="DNF_NO_LOWER_CLASS_FILTERS__0x08000000_"></span><span id="dnf_no_lower_class_filters__0x08000000_"></span><span id="DNF_NO_LOWER_CLASS_FILTERS__0X08000000_"></span>**DNF \_ \_ \_ 类 \_ 筛选器不 (0x08000000)**  
设备的类筛选器类型没有注册表项。

<span id="DNF_NO_SERVICE__0x10000000_"></span><span id="dnf_no_service__0x10000000_"></span><span id="DNF_NO_SERVICE__0X10000000_"></span>**DNF \_ 没有 \_ 服务 (0x10000000)**  
对于设备，没有服务的注册表项。

<span id="DNF_NO_UPPER_DEVICE_FILTERS__0x20000000_"></span><span id="dnf_no_upper_device_filters__0x20000000_"></span><span id="DNF_NO_UPPER_DEVICE_FILTERS__0X20000000_"></span>**DNF \_ \_) 的高级 \_ 设备 \_ 筛选器 (0x20000000**  
设备的设备筛选器类型的注册表项不存在。

<span id="DNF_NO_UPPER_CLASS_FILTERS__0x40000000_"></span><span id="dnf_no_upper_class_filters__0x40000000_"></span><span id="DNF_NO_UPPER_CLASS_FILTERS__0X40000000_"></span>**DNF \_ \_) 的 \_ 高级 \_ 筛选器 (0x40000000**  
设备的高级筛选器类型没有注册表项。

<span id="DNF_WAITING_FOR_FDO__0x80000000_"></span><span id="dnf_waiting_for_fdo__0x80000000_"></span><span id="DNF_WAITING_FOR_FDO__0X80000000_"></span>**DNF \_ 正在 \_ 等待 \_ FDO (0x80000000)**  
设备的枚举正在等待，直到驱动程序附加了其 FDO。

 

 





