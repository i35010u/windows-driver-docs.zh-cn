---
title: 节能与 VSync 控制
description: 节能与 VSync 控制
ms.assetid: d7ee7461-0d2a-4103-9225-57ca10a75a7a
keywords:
- 显示器驱动程序模型 WDK Windows Vista，节约了能源
- Windows Vista 显示器驱动程序模型 WDK，节约了能源
- 显示驱动程序模型 WDK Windows Vista 的 VSync 控制
- Windows Vista 显示器驱动程序模型 WDK 的 VSync 控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88d614b49dc71f5f222cd07af4454b9ab66e64db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351453"
---
# <a name="saving-energy-with-vsync-control"></a>节能与 VSync 控制


若要保存的计算机上的电源，内核模式显示驱动程序可以减少发生的 VSync 监视器刷新中断的数量。

较新的处理器和平台通常使用操作系统以计算机系统处于空闲状态时节约能源。 但是，定期系统活动，例如，触发中断，导致峰值电源使用情况，并且可以防止计算机系统输入将节约能源的暂时性睡眠状态。

从 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 开始，操作系统可以关闭计数时刷新屏幕时不被从新的图形或鼠标活动的定期 VSync 中断。 通过控制 VSync 中断时间间隔，您的驱动程序可以节省大量能源。

您可以通过使用 Windows Server 2008 或更高版本 Windows 驱动程序工具包 (WDK) 的重建 Windows 显示器驱动程序模型 (WDDM) 驱动程序充分利用此功能。

### <a name="span-iddriverchangesforvsynccontrolspanspan-iddriverchangesforvsynccontrolspanwindowsvista-with-sp1-driver-changes-for-vsync-control"></a><span id="driver_changes_for_vsync_control"></span><span id="DRIVER_CHANGES_FOR_VSYNC_CONTROL"></span>Windows Vista SP1 驱动程序更改的 VSync 控制

有关驱动程序以充分利用此功能，它们必须支持**VSyncPowerSaveAware**中的成员[ **DXGK\_VIDSCHCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff562863)结构，它是在 Windows Vista SP1 中引入。 请按照 WDDM 的现有驱动程序必须使用重新编译**VSyncPowerSaveAware**通过使用 Windows Server 2008 或更高版本的 WDK 的成员。

Windows Vista sp1 或更高版本系统与遵循 WDDM 和支持此功能的驱动程序将关闭计数功能的 VSync 中断发生任何 GPU 活动 10 个连续时间段内 1/Vsync，其中 VSync 是监视器的刷新频率。 如果垂直同步速率是 60 赫兹 (Hz)，VSync 中断发生一次每隔 16 毫秒。 因此，如果没有屏幕更新，VSync 中断处于关闭状态后 160 毫秒。 GPU 活动继续时，如果 VSync 中断再次打开来刷新屏幕。

### <a name="span-idwindows8display-onlyvsyncrequirementsspanspan-idwindows8display-onlyvsyncrequirementsspanspan-idwindows8display-onlyvsyncrequirementsspanwindows8-display-only-vsync-requirements"></a><span id="Windows_8_Display-Only_VSync_Requirements"></span><span id="windows_8_display-only_vsync_requirements"></span><span id="WINDOWS_8_DISPLAY-ONLY_VSYNC_REQUIREMENTS"></span>Windows 8 仅显示垂直同步要求

从 Windows 8 中，是可选的[内核模式仅显示驱动程序 (KMDOD)](https://msdn.microsoft.com/library/windows/hardware/jj673962)以支持垂直同步功能，按如下所示：

<span id="Display-only_driver_supports_VSync_control"></span><span id="display-only_driver_supports_vsync_control"></span><span id="DISPLAY-ONLY_DRIVER_SUPPORTS_VSYNC_CONTROL"></span>仅显示驱动程序支持的 VSync 控制  
如果 KMDOD 支持的 VSync 控制功能，它必须实现两者[ *DxgkDdiControlInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559602)并[ *DxgkDdiGetScanLine* ](https://msdn.microsoft.com/library/windows/hardware/ff559668)函数，而必须提供有效的函数指针，指向这两个函数中[ **KMDDOD\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/hh451571)结构。

在这种情况下还必须实现 KMDOD [ *DxgkDdiInterruptRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff559680)并[ *DxgkDdiDpcRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff559645)以便函数向操作系统报告的垂直同步中断。

此外，值**PixelRate**， **hSyncFreq**，并**vSyncFreq**的成员[ **DISPLAYCONFIG\_视频\_信号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554007)结构不能为**D3DKMDT\_频率\_NOTSPECIFIED**。

<span id="Display-only_driver_does_not_support_VSync_control"></span><span id="display-only_driver_does_not_support_vsync_control"></span><span id="DISPLAY-ONLY_DRIVER_DOES_NOT_SUPPORT_VSYNC_CONTROL"></span>仅显示驱动程序不支持的 VSync 控制  
如果 KMDOD 不支持的 VSync 控制功能，它不必须实现[ *DxgkDdiControlInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559602)或[ *DxgkDdiGetScanLine* ](https://msdn.microsoft.com/library/windows/hardware/ff559668)函数，必须提供有效的函数指针中的这些函数的任一[ **KMDDOD\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/hh451571)结构。

在这种情况下 Microsoft DirectX 图形内核子系统模拟 VSync 中断和基于当前的模式和最后一个的模拟垂直同步时扫描行的值。

此外，值**PixelRate**， **hSyncFreq**，并**vSyncFreq**的成员[ **DISPLAYCONFIG\_视频\_信号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554007)结构必须设置为**D3DKMDT\_频率\_NOTSPECIFIED**。

如果不满足这些条件，DirectX 图形内核子系统将加载 KMDOD。

### <a name="span-idregistrycontrolspanspan-idregistrycontrolspan-registry-control"></a><span id="registry_control"></span><span id="REGISTRY_CONTROL"></span> 注册表控件

对于 Windows Vista SP1 和更高版本的 Windows 操作系统中，默认 VSync 空闲超时值是 10 个 VSync 句点。 （可选） 对于测试目的，可通过使用注册表设置控制超时值。

**重要**  以避免应用程序兼容性问题，请不要更改生产驱动程序中的默认注册表设置。

 

<span id="Key_Path_"></span><span id="key_path_"></span><span id="KEY_PATH_"></span>项路径：  
**RTL\_REGISTRY\_CONTROL\\GraphicsDrivers\\Scheduler**

完整路径：  
**[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\GraphicsDrivers\\Scheduler]**

<span id="Key_Value_"></span><span id="key_value_"></span><span id="KEY_VALUE_"></span>密钥值：  
**VsyncIdleTimeout**

<span id="ValueType_"></span><span id="valuetype_"></span><span id="VALUETYPE_"></span>ValueType:  
**REG\_DWORD**

<span id="Value_"></span><span id="value_"></span><span id="VALUE_"></span>值：  
10 = 默认值

<span id="Value_"></span><span id="value_"></span><span id="VALUE_"></span>值：  
0 = 禁用 VSync 控制 (会产生相同的行为与 Windows Vista 相同)



 

 





