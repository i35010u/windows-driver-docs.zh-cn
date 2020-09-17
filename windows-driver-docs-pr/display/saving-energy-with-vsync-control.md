---
title: 节能与 VSync 控制
description: 节能与 VSync 控制
ms.assetid: d7ee7461-0d2a-4103-9225-57ca10a75a7a
keywords:
- 显示驱动程序模型 WDK Windows Vista，节能
- Windows Vista 显示器驱动程序模型 WDK，节能
- 显示驱动程序模型 WDK Windows Vista，VSync 控件
- Windows Vista 显示器驱动程序模型 WDK，VSync 控件
ms.date: 10/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 708042753e9456548d77b3b5d9f85ffd1f42c8f5
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715118"
---
# <a name="saving-energy-with-vsync-control"></a>节能与 VSync 控制

为了节省计算机上的电源，内核模式显示驱动程序可以减少发生的 VSync 监视器刷新中断数。

当计算机系统空闲时，较新的处理器和平台通常与操作系统结合使用，以节省能源。 但定期发生的系统活动（例如中断中断）将导致高峰功率消耗，并可防止计算机系统进入暂时睡眠状态，从而节省能源。

从带有 Service Pack 1 的 Windows Vista (SP1) 和 Windows Server 2008 开始，当屏幕不是从新图形或鼠标活动中刷新时，操作系统可以关闭周期性 VSync 中断计数。 通过控制 VSync 中断间隔，驱动程序可以节省大量能源。

可以通过使用 windows Server 2008 或更高版本的 Windows 驱动程序工具包 (WDK) ，使用 windows Server 或更高版本重新生成 Windows 显示驱动程序模型 (WDDM) 驱动程序来利用此功能。

## <a name="windowsvista-with-sp1-driver-changes-for-vsync-control"></a>Windows Vista SP1 驱动程序更改 VSync 控件

为了使驱动程序能够利用此功能，这些驱动程序必须支持 Windows Vista SP1 中引入的[DXGK_VIDSCHCAPS](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)结构中的**VSyncPowerSaveAware**成员。 必须使用 **VSyncPowerSaveAware** 成员通过使用 Windows Server 2008 或更高版本的 WDK 重新编译遵循 WDDM 的现有驱动程序。

如果 Windows Vista SP1 或更高版本的驱动程序的驱动程序遵循 WDDM 并且支持此功能，则将关闭 VSync 中断的计数功能，前提是10个连续的 1/Vsync （其中 VSync 是监视器的刷新频率）。 如果 VSync 速率为60赫兹 (Hz) ，则 VSync 中断每16毫秒进行一次。 因此，在没有屏幕更新时，VSync 中断将在160毫秒后关闭。 如果 GPU 活动恢复，VSync 中断将再次打开以刷新屏幕。

## <a name="display-only-vsync-requirements-for-windows-8-and-later-versions"></a>仅显示 Windows 8 及更高版本的 VSync 要求

在 windows 8 及更高版本的 Windows 操作系统中，对于 [仅限内核模式显示的驱动程序， (KMDOD) ](/windows-hardware/drivers/ddi/index) 以支持 VSync 功能，这是可选的，如下所示：

- **仅显示驱动程序支持 VSync 控件**

  如果 KMDOD 支持 VSync 控件功能，则它必须实现 [*DxgkDdiControlInterrupt*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt) 和 [*DxgkDdiGetScanLine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline) 函数，并且必须在 [KMDDOD_INITIALIZATION_DATA](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_kmddod_initialization_data) 结构中提供这两个函数的有效函数指针。

  在这种情况下，KMDOD 还必须实现 [*DxgkDdiInterruptRoutine*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine) 和 [*DxgkDdiDpcRoutine*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dpc_routine) 函数以便向操作系统报告 VSync 中断。

  此外，不能**D3DKMDT_FREQUENCY_NOTSPECIFIED** [DISPLAYCONFIG_VIDEO_SIGNAL_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_video_signal_info)结构的**PixelRate**、 **hSyncFreq**和**vSyncFreq**成员的值。

- **仅显示驱动程序不支持 VSync 控件**

  如果 KMDOD 不支持 VSync 控件功能，则它不能实现 [*DxgkDdiControlInterrupt*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt) 或 [*DxgkDdiGetScanLine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline) 函数，并且不能在 [KMDDOD_INITIALIZATION_DATA](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_kmddod_initialization_data) 结构中提供任何这些函数的有效函数指针。

  在这种情况下，Microsoft DirectX 图形内核子系统模拟 VSync 中断的值，并基于当前模式和最后一次模拟 VSync 的时间扫描行。

  此外， [DISPLAYCONFIG_VIDEO_SIGNAL_INFO](/windows/win32/api/wingdi/ns-wingdi-displayconfig_video_signal_info)结构的**PixelRate**、 **hSyncFreq**和**vSyncFreq**成员的值必须设置为**D3DKMDT_FREQUENCY_NOTSPECIFIED**。

如果未满足这些条件，DirectX 图形内核子系统将不会加载 KMDOD。

## <a name="registry-control"></a>注册表控件

对于 Windows Vista SP1 及更高版本的 Windows 操作系统，默认的 VSync 空闲超时值为 10 VSync。 （可选）出于测试目的，可以使用注册表设置来控制超时。

> [!IMPORTANT]
> 若要避免应用程序兼容性问题，请不要更改生产驱动程序中的默认注册表设置。

注册表项路径：  
**RTL_REGISTRY_CONTROL \GraphicsDrivers\Scheduler**

完整路径：  
**[HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler]**

项值：  
**VsyncIdleTimeout**

ValueType  
REG_DWORD 

值：  
10 = 默认值

值：  
0 = 禁用 VSync 控件 (生成与 Windows Vista 相同的行为) 