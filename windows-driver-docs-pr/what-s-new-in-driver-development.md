---
title: 驱动程序开发中的新增功能
description: 本部分介绍 Windows 10 中驱动程序开发的新增功能。
ms.assetid: 5502AAF9-2400-4338-A646-C746B29F9A44
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: d6313e63b154a6768f1dab068fbafddbeeb540cf
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063945"
---
# <a name="whats-new-in-driver-development"></a><a name="top"></a>驱动程序开发中的新增功能

本部分提供有关 Windows 10 中 Windows 驱动程序开发的新增功能和更新的信息。

## <a name="whats-new-in-windows-10-version-2004-latest"></a>Windows 10 版本 2004（最新版）的最近更新

本部分介绍了 Windows 10 版本 2004（Windows 10 2020 年 5 月更新）中关于驱动程序开发的新功能和更新。

### <a name="windows-drivers"></a>Windows 驱动程序

Windows 10 版本 2004 是通用驱动程序的过渡版本。 在此版本中，通用驱动程序仍存在，但正在被 Windows 驱动程序所取代。 Windows 驱动程序是有一些额外要求的通用驱动程序。

Windows 驱动程序与 Windows 桌面驱动程序是不同的。 Windows 驱动程序在 Windows 10X 和 Windows 10 桌面版中运行，而 Windows 桌面驱动程序只在 Windows 10 桌面版中运行。

对于版本 2004，无需对通用驱动程序进行任何更改，但文档现已发布，以便你能够提前为即将发生的更改做好计划。

若要了解如何生成、安装、部署和调试 Windows 驱动程序，请参阅 [Windows 驱动程序入门](./develop/getting-started-with-windows-drivers.md)。

### <a name="windows-hardware-error-architecture-whea"></a>Windows 硬件错误体系结构 (WHEA)

WHEA 新增了一个接口 (v2)。 若要了解如何注册为错误源并报告错误，请参阅[在 Windows 10 中使用 WHEA](whea/using-whea-on-windows-10.md)。

### <a name="display-and-graphics-drivers"></a>显示驱动程序和图形驱动程序

Windows 10 版本 2004 中提供了几个新的和增强的显示驱动程序和图形驱动程序功能，其中包括 D3D12 网格着色器支持、采样器支持、光线跟踪扩展、视频运动估计，以及视频的受保护资源支持。 有关这些新功能的详细信息，请参阅 [Windows 10 显示驱动程序和图形驱动程序的新增功能](./display/what-s-new-for-windows-10-display-and-graphics-drivers.md)。

### <a name="storage-drivers"></a>存储驱动程序

存储微型端口驱动程序现在可以获取和设置有关设备的内部状态的详细信息，包括重置设备的功能。 请从参阅 [**IOCTL_STORAGE_GET_DEVICE_INTERNAL_LOG**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_device_internal_log) 和 [**StorPortHardwareReset**](/windows-hardware/drivers/ddi/storport/nf-storport-storporthardwarereset) 开始了解相关信息。

### <a name="windows-debugger"></a>Windows 调试器

#### <a name="windbg-preview"></a>WinDbg 预览版

[WinDbg 预览版](./debugger/debugging-using-windbg-preview.md)的更新包含新功能，例如 [WinDbg 预览版 - 时间线](./debugger/windbg-timeline-preview.md)。 可通过时间旅行时间线直观显示时间旅行代码执行跟踪。

#### <a name="stop-codes"></a>停止代码

- 更新 [Bug 检查代码参考](./debugger/bug-check-code-reference2.md)主题，向 [Bug 检查 0x1A：MEMORY_MANAGEMENT](./debugger/bug-check-0x1a--memory-management.md) 和 [Bug 检查 0xC4：DRIVER_VERIFIER_DETECTED_VIOLATION](./debugger/bug-check-0xc4--driver-verifier-detected-violation.md) 主题添加了新参数。

- 新的停止代码，例如 [Bug 检查 0x1DA：HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR](./debugger/bug-check-0x1da--hal-blocked-processor-internal-error.md)、[Bug 检查 0x1A2：WIN32K_CALLOUT_WATCHDOG_BUGCHECK](./debugger/bug-check-0x1a2--win32k-callout-watchdog-bugcheck.md) 和 [Bug 检查 0x119：VIDEO_SCHEDULER_INTERNAL_ERROR](./debugger/bug-check-0x119---video-scheduler-internal-error.md)。

### <a name="driver-security"></a>驱动程序安全性

更新了[驱动程序安全清单](./driversecurity/driver-security-checklist.md) 以使用 BinSkim 工具。

## <a name="related-topics"></a>“相关主题”

若要了解旧版 Windows 中关于驱动程序的最近更新，请参阅以下页面：

* [Windows 10 版本 1903 的驱动程序开发变更](driver-changes-for-windows-10-version-1903.md)
* [Windows 10 版本 1809 的驱动程序开发变更](driver-changes-for-windows-10-version-1809.md)
* [Windows 10 版本 1803 的驱动程序开发变更](driver-changes-for-windows-10-version-1803.md)
* [Windows 10 版本 1709 的驱动程序开发变更](driver-changes-for-windows-10-version-1709.md)

[返回页首](#top)

## <a name="deprecated-features"></a>已弃用的功能

下表描述了 Windows 10 中已删除的 Windows 驱动程序开发功能。

| 驱动程序技术 | 功能 | 弃用该功能的版本 |
|---|---|---|
| GNSS/定位 | [Windows 8.1 的地理位置驱动程序示例](./gnss/sensors-geolocation-driver-sample.md)和相关文档 | Windows 10 版本 1709 |
| 移动运营商方案（网络） | [AllowStandardUserPinUnlock](./mobilebroadband/allowstandarduserpinunlock.md) | Windows 10 版本 1709 |
| 扫描/成像 | [WSD（设备 Web 服务）质询器](./image/challenging-a-disconnected-scanner-with-the-wsd-challenger.md)功能和相关文档 | Windows 10 版本 1709 |
|移动运营商| 由于 MO UWP APPS 和 COSA 的推出，包含 Sysdev 元数据包的移动宽带应用体验已弃用。 | Windows 10 版本 1803|