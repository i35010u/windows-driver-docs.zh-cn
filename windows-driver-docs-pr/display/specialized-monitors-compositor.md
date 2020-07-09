---
title: 为 HMDs 和专用监视器生成自定义组合器应用
description: 为 HMDs 和专用监视器生成自定义组合器应用
keywords:
- 显示设备 WDK
- 监视驱动程序 WDK
- 显示驱动程序 WDK，监视驱动程序
- monitors
- HMD
- 虚拟现实
ms.author: windowsdriverdev
ms.date: 7/8/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 2bc9410394c29501a528a1cfdeb78fad4be52154
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141238"
---
# <a name="building-a-custom-compositor-app-for-hmds-and-specialized-monitors"></a>为 HMDs 和专用监视器生成自定义组合器应用

排序器[API](https://docs.microsoft.com/uwp/api/windows.devices.display.core)是用于在 Windows 中枚举、配置和驱动显示适配器并显示目标的所有其他公共 api 的第三方和内部操作系统组件的低级 WinRT api。 其思路是将显示控制器视为单独的 "引擎"，类似于3D 引擎和 GPU 上的媒体引擎。 此 API 负责：

* 应答有关显示硬件的查询（如功能和可能的显示模式）
* 正在应答有关当前配置的查询
* 设置显示硬件上的属性（如显示模式）
* 配置显示硬件（已连接监视器的分辨率、其线路格式等）
* 分配和扫描称为 "主副本" 的特殊 GPU 面
* 允许 Direct3D 和 Windows. Core Api 之间的互操作（例如，共享表面、时限）

值得一提的是，什么是**不**显示的 Windows。 Core：

* 它不是应用程序使用的 API，用于在窗口中显示内容。 应用仍使用 DXGI、XAML、DirectComposition、GDI 等。
* 它不是用于显示内容全屏的游戏所使用的 API。 应用程序仍使用 DXGI，Win32 应用仍使用 Hwnd，UWP 应用始终显示 CoreWindow 中的内容。

此 API 适用于仅驱动专用硬件的组合器应用。

![API 体系结构层](images/specialized-displays-layers.png)


## <a name="scenarios-for-building-custom-compositors"></a>用于生成自定义排序器的方案

在以下方案中，可以使用 Windows. Core Api：
* 虚拟和扩充的现实显示，需要专有的组合器直接驱动显示控制器，并获得与 Windows 桌面分开的计时和模式配置的精细控制。
* 专用的显示硬件方案，需要在商业设置中对显示屏进行专用控制。 例如，由于硬件弯曲、灰度显示等，Windows 桌面无法正确呈现此类显示器的情况。
* 专门的 "装置" 方案，在此方案中，监视器可能会完全专用于应用程序，而不会在很长一段时间内对 Windows 桌面体验产生任何干扰（如专用视频监视器）。

API 完成此操作的方法如下：
* 提供对完整显示模式信息的精细控制，包括有线格式、HDR 等。
* 使用范围进行同步表示允许合成器在进程或子组件之间链接表示，几乎不会产生任何性能开销。
* 提高了查询和配置基础视频提供网络（VidPN）的能力，以允许系统组件和低级别组合组件以不容易出错且更具扩展性的方式执行更复杂的操作。

请注意，此 API 只适用于一*组特别*适用于专用硬件的第三方用例。 它的使用非常受限于声明自身需要此 API 功能的硬件。 因此，开发人员需要一定程度的硬件概念，并且合作伙伴应直接与 Microsoft 联系以帮助解决问题。

## <a name="hardware-requirements"></a>硬件要求

第三方自定义排序器只能获取已预先指定为 HMDs 或 "专用" 显示的显示。 必须通过以下两种方式之一提供此指定：
* **EDID 扩展**-为永久性使用而设计的自定义显示设备（如 HMDs、X 光监视器、视频墙壁或其他专用方案）应该实现[Microsoft EDID Extension for HMDs 和专用显示器](specialized-monitors-edid-extension.md)。
* **用户替代**-对于使用现成监视器的自定义硬件安装，Windows 提供了用于将监视器指定为 "专用化" 的 UI 切换。

**不**能通过覆盖软件中的 EDID 将显示指定为 HMDs 或专用显示。

## <a name="roadmap-for-implementing-a-custom-compositor"></a>用于实现自定义组合器的路线图

实现自定义组合器可以分为多个阶段：

1. 枚举并发现关联的 HMDs 或专用显示
2. 获取所选显示的所有权
2. 配置所有选定显示器的模式
4. 创建用于向显示器呈现帧的资源
5. 呈现内容和计划框架演示

## <a name="comparison-of-display-related-apis"></a>与显示相关的 Api 的比较

| API | 目的和目标受众 |
|-----|-----------------------------|
| `Windows.Graphics.Display.DisplayInformation` | 用于检索 CoreWindow 的呈现和布局属性。 |
| `Windows.Graphics.Display.Core.HdmiDisplayInformation` | 用于枚举和设置受约束的模式集的仅供 Xbox 使用的 API。 针对 Xbox media 应用方案进行了高度专用化。 |
| `Windows.Devices.Display.DisplayMonitor` | 用于查询物理监视器设备的属性。 不公开有关操作系统如何配置或当前正在使用监视器的任何运行时信息。 |
| `EnumDisplayDevices`, `EnumDisplayMonitors`, `EnumDisplaySettings` | 用于查询 HMONITORs、GDI 设备和物理监视器映射的旧版 Win32 Api。 此处返回的信息是高度虚拟化的，并保持应用程序兼容性。 |
| Direct3D | 用于将像素内容呈现为 GPU 面并在 GPU 上执行计算。 |
| DXGI 交换链 | 用于开窗和 "无边框窗口" 演示。 应用交换链内容通过系统组合器（DWM）流动。 |
| DXGI 输出枚举 | 提供 HMONITORs 周围的 DXGI 包装。 |
| `QueryDisplayConfig`, `SetDisplayConfig`, `DisplayConfigGetDeviceInfo`, `DisplayConfigSetDeviceInfo` | 用于配置显示拓扑的 Win32 Api。 不提供枚举多个模式的机制，但包含一组有关当前配置和设置的丰富信息。 但并非所有模式的新属性都由这些 Api 公开。 |
| `Windows.Devices.Display.Core`**（本文档）** | 用于枚举目标、枚举模式、配置模式、为演示分配 GPU 图面以及显示要显示的内容。 |

## <a name="display-configuration-overview"></a>显示配置概述

### <a name="physical-hardware-enumeration"></a>物理硬件枚举

Windows. Core API 具有用于表示物理硬件对象的各种对象。 `DisplayAdapter`通常（但不总是）物理硬件设备，如 PCI Express 连接的 gpu 或 CPU 上的集成 GPU。 DisplayTargets 表示可从 GPU 连接到的物理连接器（如 HDMI、VGA、DisplayPort 等）。 这可能包括具有内部监视器（便携式计算机、平板电脑等）的设备的内部非用户可见连接。 软件中可能会有更多的 DisplayTargets，而不是用户一次可以物理连接。 例如，由于 DisplayPort 连接标准允许菊花链，因此 GPU 驱动程序通常会枚举每个物理端口的多个 DisplayPort 目标，以便为链接的监视器提供帐户。

![硬件拓扑图](images/specialized-displays-hardware.png)

### <a name="objects-for-setting-modes"></a>用于设置模式的对象

用于枚举 DisplayTargets、设置和查询模式等。与 DisplayTargets 的连接由 DisplayPaths 表示。 克隆组由 DisplayViews 表示，并聚合到 DisplayState 中。 因此，一个 DisplayState 对象可以代表一组可发送到多个监视器的驱动程序的模式状态。

![模式拓扑图](images/specialized-displays-state-objects.png)

### <a name="atomic-state-for-mode-configuration-and-enumeration"></a>模式配置和枚举的原子状态

Windows. Core API 旨在确保排序器能够以原子方式获取对各种系统显示状态的访问权限，并具有定义完善的 "不过期" 行为。 这一点很重要，因为 Gpu 是共享资源，具有非常紧张的带宽和电源限制。 在新式系统中，设备可能会在任何时间到达/脱离，而其他因素可能会影响可用显示模式的列表（例如，停靠/移除、休眠状态，另一个组件更改另一条路径的模式）。 因此，排序器可以通过使用 Windows. Display API 和以下建议的模式来灵活地更改系统配置，这一点很重要。

因此，Windows. Core API 提供了简单的事务读修改-提交模型，类似于数据库。 客户端可以在系统中以原子方式读取显示设备的 DisplayState 对象。 所有对象都是不可变的，或者提供定义完善的 Api，用于将状态更新/提交到系统。 在调用 DisplayState TryApply 之前，不会进行更改，这会将对系统的更改提交给系统。 提交/应用对 DisplayState 所做的更改可能会失败且不会产生任何影响，也不会成功应用完整更改。

利用 API 的原子性功能：

* 在可重试循环**中编写任何**模式配置逻辑。
* **请在**每个循环中的模式配置的开头创建新的 DisplayState。
* **Do** [`FailIfStateChanged`](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystateapplyoptions) 调用 DisplayState 时，请使用标志来检测系统状态是否不再与创建 DisplayState 时相同。 这使您有机会重试该操作。 如果操作失败，则 `SystemStateChanged` 重试整个循环。
* **不要**混合使用 Windows 的其他 API （DXGI、GDI 等）来读取或更改状态，因为它们可能没有相同的原子保证。

```C++
#include <winrt\Windows.Devices.Display.Core.h>
using namespace winrt::Windows::Devices::Display::Core;
...

// Create a DisplayManager
DisplayManager manager = DisplayManager::Create(DisplayManagerOptions::EnforceSourceOwnership);

// Loop around trying to acquire a target and set a mode
bool shouldRetry;
do
{
    shouldRetry = false;

    // ... Find the target that you want to use
    auto targets = manager.GetCurrentTargets();
    DisplayTarget selectedTarget = ...;

    auto stateCreationResult = manager.TryAcquireTargetsAndCreateEmptyState(
        winrt::single_threaded_vector<DisplayTarget>({ selectedTarget }));

    if (stateCreationResult.ErrorCode() != DisplayManagerResult::Success)
    {
        winrt::check_hresult(stateCreationResult.ExtendedErrorCode());
    }

    auto state = stateCreationResult.State();
    DisplayPath newPath = state.ConnectTarget(selectedTarget);

    // ... Configure the path

    auto applyResult = state.TryApply(DisplayStateApplyOptions::FailIfStateChanged);

    if (applyResult.Status() == DisplayStateOperationStatus::SystemStateChanged)
    {
        shouldRetry = true;
    }
    else if (applyResult.Status() != DisplayStateOperationStatus::Success)
    {
        winrt::check_hresult(applyResult.ExtendedErrorCode());
    }

} while (shouldRetry);
```

以下 Api 以原子方式从系统读取状态：

* **DisplayManager**
    * [GetCurrentTargets](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.getcurrenttargets)
    * [GetCurrentAdapters](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.getcurrentadapters)
    * [TryReadCurrentStateForAllTargets](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.tryreadcurrentstateforalltargets) /[TryAcquireTargetsAndReadCurrentState](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.tryacquiretargetsandreadcurrentstate)
* **DisplayState**
    * [IsStale](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystate.isstale)
    * [TryFunctionalize](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystate.tryfunctionalize)
* **DisplayPath**
    * [FindAllModes](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaypath.findmodes)
* **DisplayTarget**
    * [DisplayTarget.IsStale](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaytarget.isstale)

以下 Api 将状态传回系统：

* **DisplayManager**
    * [TryAcquireTarget](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.tryacquiretarget) /[ReleaseTarget](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.releasetarget) （并通过方法获取目标 `TryAcquireTargetsAnd*` ）–从系统获取 DisplayTargets 的所有权。
* **DisplayState**
    * [TryApply](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystate.tryapply) –通过显示驱动程序，通过设置或清除系统中所有拥有目标的模式来更新当前系统显示状态。

## <a name="known-limitations"></a>已知的限制

在 Windows 10 版本2004中，Windows. Core API 具有几个已知限制：

* 当前无法解决间接显示驱动程序（例如，Miracast、USB 显示适配器、软件驱动程序）。 `DisplayManager.CreateDisplayDevice`传递间接显示适配器时，将失败。

## <a name="sample-code"></a>示例代码

有关示例应用程序，请参阅 " [Windows. 磁芯" 自定义组合器示例](https://github.com/microsoft/Windows-classic-samples/tree/master/Samples/DisplayCoreCustomCompositor)。