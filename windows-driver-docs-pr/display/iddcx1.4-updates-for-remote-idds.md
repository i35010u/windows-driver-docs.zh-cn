---
title: 远程 IDD 的 IddCx 1.4 更新
description: 远程间接显示驱动程序的 IddCx 版本1.4 更新
ms.assetid: 4e065381-f1cd-401a-9844-f85eaf414b5f
ms.date: 09/28/2020
keywords:
- 远程间接显示驱动程序，IddCx 版本1.4 及更高版本
- 远程 IDD，IddCx 版本1.4 及更高版本
- 远程间接显示驱动程序
- 远程 IDD
ms.localizationpriority: medium
ms.openlocfilehash: d066cbc2cd36d4768094a324a84ae793adda38f8
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732551"
---
# <a name="iddcx-14-updates-for-remote-idds"></a>远程 IDD 的 IddCx 1.4 更新

以下 IddCx 版本1.4 更新仅适用于远程间接显示驱动程序 (IDDs) 。

远程 IDD 开发人员还应查看适用于 [控制台和远程 IDDs 的 IddCx 1.4 更新](iddcx1.4-updates-for-console-and-remote-idds.md) 以获取其他更新。

## <a name="declare-a-remote-idd-for-remote-sessions"></a>为远程会话声明远程 IDD

IDD 声明它要通过设置[**IDDCX_ADAPTER_CAPS**](/windows-hardware/drivers/ddi/iddcx/ns-iddcx-iddcx_adapter_caps)中的**IDDCX_ADAPTER_FLAGS_REMOTE_SESSION_DRIVER**位来创建远程 ID 适配器 **。** 调用[**IddCxAdapterInitAsync**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)时的标志字段。  OS 跟踪是否正在加载 IDD，因为远程桌面堆栈连接到远程会话，并且在以下两种情况下将无法 **IddCxAdapterInitAsync** 调用：

1. 未为远程会话的 OS 远程桌面堆栈创建的设备设置 IDD **IDDCX_ADAPTER_FLAGS_REMOTE_SESSION_DRIVER**
2. 不是由 OS 远程桌面堆栈创建的设备的 IDD 集**IDDCX_ADAPTER_FLAGS_REMOTE_SESSION_DRIVER**

### <a name="installation-recommendations-for-remote-idds"></a>远程 IDDs 的安装建议

使用 UMDF，驱动程序可以在其 INF 文件中使用**UmdfHostProcessSharing**和**DeviceGroupId**之类的指令控制[设备池选项](../wdf/using-device-pooling-in-umdf-drivers.md)。 由于某些锁争用问题，强烈建议 remote IDDs 将 **UmdfHostProcessSharing** 指令设置为 **ProcessSharingDisabled**。 此设置将为每个会话配置远程 IDD，使其在其自己的进程中。

### <a name="additional-restrictions-on-existing-iddcx-features-for-remote-idds"></a>针对远程 IDDs 的现有 IddCx 功能的其他限制

远程 IDDs 需要在[**IDDCX_ADAPTER_CAPS**](/windows-hardware/drivers/ddi/iddcx/ns-iddcx-iddcx_adapter_caps)中设置**IDDCX_ADAPTER_FLAGS_USE_SMALLEST_MODE** **。标志**字段。  这可确保不使用虚拟模式，因此，存在大小将始终与桌面分辨率匹配。 如果未设置此标志， [**IddCxAdapterInitAsync**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)将失败。

远程 IDDs 仅支持渐进式目标模式，因此 [**IDDCX_TARGET_MODE**](/windows-hardware/drivers/ddi/iddcx/ns-iddcx-iddcx_target_mode)**。TargetVideoSignalInfo. targetVideoSignalInfo. scanLineOrdering** 必须设置为 **DISPLAYCONFIG_SCANLINE_ORDERING_PROGRESSIVE**。 如果未设置此值， [**IddCxMonitorArrival**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival)将失败。

## <a name="set-the-display-configuration-for-the-remote-session"></a>设置远程会话的显示配置

当远程 IDDs 控制远程会话中的所有监视器，并且远程会话显示配置应镜像客户端时，远程 IDD 需要能够指定 OS 将在远程会话中设置的显示配置。 当会话创建为远程会话或转换到远程会话时，需要设置此显示配置。  

远程 IDD 可将远程会话期间的显示配置更新为：

* 更改当前监视器的设置 (例如，更改桌面位置、方向、物理大小或 DPI) 
* 添加/删除监视器后，通过调用[**IddCxMonitorArrival**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival) / [**IddCxMonitorDeparture**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitordeparture)设置桌面配置。 远程 IDDs 使用 **IddCxMonitorArrival** 和 **IddCxMonitorDeparture** 的方式与控制台 IDDS 相同，通知操作系统有关监视抵达和出发的信息。

下面是 OS 用于处理监视器抵达、出发和桌面配置更改的逻辑。 对于每个远程会话，操作系统将存储由远程 IDD 提供的单个当前桌面配置。 此桌面配置将为空，并且将在每次远程 IDD 成功调用 [**IddCxDisplayConfigUpdate**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterdisplayconfigupdate)时进行更新。

### <a name="when-the-driver-receives-a-new-display-configuration"></a>当驱动程序收到新的显示配置时

```
If all monitors in the new display configuration are present in the system
    If new display configuration is supported by driver (eg resolutions)
        Store new display configuration
        Set new display configuration (this will disable any active monitors
            that are not part of new configuration)

If all monitors in the new display config are not currently present in the system
    Store new display configuration
    Disable all active paths and wait for the correct set of monitors to arrive
```

### <a name="when-a-monitor-is-removed"></a>删除监视器时

```
If removed monitor is not in the current display configuration
    Remove the monitor and do not change the current desktop configuration

If removed monitor is part of the current display configuration
    Remove the monitor
    Disable all active paths and wait for the correct set of monitors to arrive
```

### <a name="when-a-monitor-arrives"></a>监视器到达时

```
If added monitor is not part of current display configuration
    Do not change the display configuration

If added monitor is part of the current display configuration
    If now all the monitors in the current display configurations are present
        Set the new display configuration
```

下面是一些简单的方案，用于说明如何使用 [**IddCxDisplayConfigUpdate**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterdisplayconfigupdate) 。

### <a name="scenario-1-a-new-session-starts-with-two-monitors-connected"></a>方案1：从两个连接的监视器开始新的会话

| 驱动程序操作 | 当前显示拓扑 | 当前连接的监视器| 当前处于活动状态的监视器 | 说明 |
| ------------------------- | ---------- | ---------- | ---------- | -------------------- |
|                           | 无       | 无       | 无       | 会话启动配置 |
| IddCxMonitorArrival (Mon1)  | 无       | Mon1       | 无       | 无活动显示配置，因此没有任何更改 |
| IddCxMonitorArrival (Mon2)  | 无       | Mon1, Mon2 | 无       | 在显示配置中仍无更改 |
| IddCxDisplayConfigUpdate  | Mon1, Mon2 | Mon1, Mon2 | Mon1, Mon2 | 在所有监视器均已连接的情况下，设置配置 |

注意：在为同一结果添加监视器之前，驱动程序可能已调用 **IddCxDisplayConfigUpdate** 。

### <a name="scenario-2-add-a-third-monitor-to-scenario-1-and-make-it-active"></a>方案2：将第三个监视器添加到方案1并使其处于活动状态

| 驱动程序操作 | 当前显示拓扑 | 当前连接的监视器| 当前处于活动状态的监视器 | 注释 |
| ------------------------- | ---------- | ---------- | ---------- | -------------------- |
| IddCxMonitorArrival (Mon3)  | Mon1, Mon2       | Mon1, Mon2, Mon3 | Mon1, Mon2       | 没有更改显示配置 |
| IddCxDisplayConfigUpdate  | Mon1, Mon2, Mon3 | Mon1, Mon2, Mon3 | Mon1, Mon2, Mon3 | 新建配置集 |

### <a name="scenario-3-remove-a-monitor-from-an-active-configuration"></a>方案3：从活动配置中删除监视器

| 驱动程序操作 | 当前显示拓扑 | 当前连接的监视器| 当前处于活动状态的监视器 | 注释 |
| --------------------------- | ---------------- | ---------------- | ---------------- | -------------------- |
|                             | Mon1, Mon2       | Mon1, Mon2       | Mon1, Mon2       | 正在启动配置 |
| IddCxDisplayConfigUpdate ( # A1  | Mon1             | Mon1, Mon2       | Mon1             | 更改配置以仅在第一次使用 Mon1 |
| IddCxMonitorDeparture (Mon2)  | Mon1             | Mon1             | Mon1             | |

### <a name="scenario-4-changing-the-mode-of-a-path-when-the-driver-only-supports-a-single-mode"></a>方案4：当驱动程序仅支持单模式时更改路径的模式

| 驱动程序操作 | 当前显示拓扑 | 当前连接的监视器| 当前处于活动状态的监视器 | 注释 |
| ------------------------------------------- | ---------------------- | ---------- | ---------- | -------------------- |
|                                             | Mon1 10x7 , Mon2 19x10 | Mon1, Mon2 | Mon1, Mon2 | 正在启动配置 |
| IddCxMonitorUpdateModes (Mon1 支持 16x9)  | 无                   | Mon1, Mon2 | 无       | Mon1 到16x9 的更新模式列表 |
| IddCxDisplayConfigUpdate ( # A1                  | Mon1 16x9，Mon2 19x10  | Mon1, Mon2 | Mon1, Mon2 | 将 Mon1 的 config 设置为16x9 |

### <a name="handling-iddcxdisplayconfigupdate-errors"></a>处理 IddCxDisplayConfigUpdate 错误

远程驱动程序需要处理来自 [**IddCxDisplayConfigUpdate**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterdisplayconfigupdate)的错误。 应为某些错误;例如，当连接使用临时会话时。

在初始配置的意外情况下，驱动程序具有如下选项：

* 调用 [**IddCxReportCriticalError**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxreportcriticalerror) 以终止驱动程序进程并断开用户会话。 建议驱动程序使用唯一的主要/次要组合，以便能够在崩溃和 Watson 报告中识别这些情况。
* 如果发生暂时性错误，请再次重试配置。
* 尝试不同的配置。

远程驱动程序可能会确定中间会话配置更改失败与初始配置故障不一样重要，因此可能永远不会调用 **IddCxReportCriticalError** 中间会话。

如果[**IddCxDisplayConfigUpdate**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterdisplayconfigupdate)返回 STATUS_GRAPHICS_INDIRECT_DISPLAY_DEVICE_STOPPED，则驱动程序不应调用[**IDDCXREPORTCRITICALERROR**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxreportcriticalerror) ，因为操作系统检测到目标会话正在断开连接，或者该会话的 IddCx 适配器正在停止，因为这是预期的。

## <a name="display-api-changes-in-an-indirect-display-remote-session"></a>显示间接显示远程会话中的 API 更改

在远程 XDDM 会话中，OS 显示控制面板不向用户提供任何控制来更改显示配置的控件。 这主要是因为远程会话桌面配置由连接客户端系统控制，而不是由会话中运行的应用程序控制。 例如，支持 Win + P 投影用户界面在远程会话中没有意义。

通常，对于远程 ID 会话：

* 显示枚举 Api 工作，包括[ **QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig)
* 显示设置 Api 不起作用。 例如，在远程会话中运行的应用程序不需要调用[**ChangeDisplaySettings**](/windows/win32/api/winuser/nf-winuser-changedisplaysettingsa) / [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig)来更改桌面配置 (例如，更改桌面位置或拓扑) 。

有趣的是，远程 XDDM 解决方案使用 **ChangeDisplaySetting** 来更改模式和桌面位置，因为这是可应用客户端更改的唯一方法。 由于远程 ID 解决方案具有 [**IddCxDisplayConfigUpdate**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterdisplayconfigupdate) 功能，因此 **ChangeDisplaySetting** 不再需要在远程 ID 会话中运行。

下表显示了 "Api" 和 "控制面板"， (CPL) 功能在 XDDM 远程会话和 WDDM 远程会话中。

| API/CPL | XDDM 远程会话 | WDDM 远程会话 |
|-| ------------------- | ------------------- |
| **显示 CPL** | 不会显示任何信息，并且会发出一条消息，指出 "无法从远程会话更改显示设置"。 | 与 XDDM 远程会话相同的行为。 |
| **Win + P UI 和功能** | UI 未显示，API 失败。 | 与 XDDM 远程会话相同的行为。 |
| **旧的显示枚举 Api (例如 EnumDisplaySettings & EnumDisplayDevices) ** | API 按预期方式工作并返回相关信息。 | 与 XDDM 远程会话相同的行为。 |
| **旧 ChangeDisplaySetting** | Works 并用于反映来自客户端的桌面更改。 | 返回应用程序兼容性的成功原因，但忽略调用且不更改任何显示配置。  IDD 将使用 **IddCxDisplayConfigUpdate** 更改桌面配置。 |
| **QueryDisplayConfig** | 失败. | 按预期方式工作。 |
| **DisplayConfigGetDeviceInfo** | 失败. | 工作并报告所需的信息。 |
| **SetDisplayConfig 和 DisplayConfigSetDeviceInfo** | 失败. | 与 XDDM 远程会话相同的行为。 |

## <a name="monitor-idle-behavior-in-an-id-remote-session"></a>监视 ID 远程会话中的空闲行为

当协议堆栈调用[**IWRdsProtocolConnectionCallback：： StopScreenUpdates**](/windows/win32/api/wtsprotocol/nf-wtsprotocol-iwrdsprotocolconnectioncallback-stopscreenupdates)来停止更新客户端屏幕时，OS 会销毁交换链，并使该会话的所有路径处于非活动状态，从而导致在[**IDDCX_PATH**](/windows-hardware/drivers/ddi/iddcx/ns-iddcx-iddcx_path)中**IDDCX_PATH_FLAGS_NONE**设置调用 IDD 的[**EVT_IDD_CX_ADAPTER_COMMIT_MODES**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_adapter_commit_modes)回调 **。** 所有路径的标志。

当协议堆栈调用 [**IWRdsProtocolConnectionCallback：： RedrawWindow**](/windows/win32/api/wtsprotocol/nf-wtsprotocol-iwrdsprotocolconnectioncallback-redrawwindow) 以再次启用更新时，操作系统将使用 IDD 的 **EVT_IDD_CX_ADAPTER_COMMIT_MODES** 回调来设置新的活动路径，并将创建新的交换链。

## <a name="disconnect-behavior-in-an-id-remote-session"></a>ID 远程会话中的断开连接行为

当用户断开与远程会话的连接时，OS 会销毁为该会话托管远程 ID 设备的 devnode，从而导致该会话 PnpStopped 的远程 ID 适配器。 UMDF 将调用远程 IDD 的 [**EVT_WDF_DEVICE_D0_EXIT**](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调。

如果会话以远程方式再次连接，则操作系统将为该会话的远程 IDD 创建新的 devnode。 远程 IDD 应再次通过正常启动序列，初始化适配器，然后添加监视器等。