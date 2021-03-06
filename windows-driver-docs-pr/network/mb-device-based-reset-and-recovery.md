---
title: MB 基于设备的重置和恢复
description: MB 基于设备的重置和恢复
keywords:
- MB 基于设备的重置和恢复、基于移动宽带设备的重置和恢复、移动宽带微型端口驱动程序基于设备的重置和恢复
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 6022048ec3c2196ab685c0d2275abc7b170b196a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248663"
---
# <a name="mb-device-based-reset-and-recovery"></a>MB 基于设备的重置和恢复

移动宽带 (MB 或 MBB) 基于设备的重置和恢复，是 Windows 10 版本1809及更高版本中的一项技术，为 MBB 设备和驱动程序引入了强大的重置恢复机制。 这种机制可让 MBB 设备避免发生故障、连接断开或操作命令的故障，最终使用户体验无缝发生（如果发生错误）并降低不得不重新启动系统的机会。 

基于设备的重置和恢复可以通过或不带固件依赖项实现。 IHV 或 OEM 合作伙伴可以使用支持的设备或固件级重置机制来扩展所有 Windows 电脑上可用的基于软件的重置机制，以提高恢复成功的速度。

## <a name="mb-device-based-reset-and-recovery-architecture-overview"></a>MB 基于设备的重置和恢复体系结构概述

Windows MBB 服务使用标准 [移动宽带接口模型](https://www.usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement) （ (MBIM) 接口，此接口是在 USB 传输扩展 NCM 规范的基础上构建的，它可初始化和控制移动设备。 发送到 IHV 设备的每个命令都通过收件箱 Windows MBB 类驱动程序发送为 MBIM 命令。 使用 MBIM 协议交换初始化蜂窝调制解调器后，可以在主机、调制解调器和网络之间启动数据路径。 发送到移动电话设备的任何其他控件将通过 MBIM 协议进行并行传输。 

在 MBIM 控制路径和数据路径上都可能会发生许多故障。 在 Windows 10 版本1809之前的 Windows 版本中，内置了简单的错误处理机制。 每当发送 MBIM 命令并且设备变得无响应时，该机制会尝试通过发送 MBIM reset 命令重置设备。 但是，因为故障通常是由于第一次 MBIM 接口无响应而导致的，所以此重置并不总是有效。 此外，该机制不会解决可能出现的其他故障，例如数据路径故障导致连接断开。 

MB 基于设备的重置和恢复引入了一个集中式框架，用于检测更大的一组故障并使用一组渐进有影响力重置来协调恢复。 如果设备支持设备级重置，MB 基于设备的重置和恢复将在所有基于软件的重置都用尽后合并设备级重置。 重置和恢复框架将重新定义，并根据 MBIM 命令响应能力替换现有的重置机制。  

MB 基于设备的重置和恢复检测和尝试解决以下类型的故障：

| 故障区域        | 失败描述                                         |
|------------------------|-------------------------------------------------------------|
| 控制路径           | <ul><li>在 MBIM 协议路径上检测到挂起状态。 有关挂起检测的详细信息，请参阅 [MB 挂起检测](mb-hang-detection.md)。</li><li>因状态和/或信息不正确而导致的 MBB 响应失败。</li></ul> |
| 数据路径              | <ul><li>设备端故障导致数据路径故障。 例如，终结点未响应数据流量，损坏的数据来自 PHY，等等。</li><li>调制解调器/网络故障。 例如，网络不响应 IP 流量、DNS 故障、数据包丢失，等等。</li></ul> |

某些故障无法从恢复角度进行操作，包括但不限于：

- 预配或与激活相关的问题，例如缺少 COSA 设置或 MO 启动的服务拒绝
- 由于驱动程序初始化失败导致的控制路径问题 (与电源或硬件相关的) 或软件 bug

但是，一旦检测到可操作的故障，基于 MB 设备的重置和恢复将尝试以下重置机制。 "重置" 选项按 Windows 执行的顺序列出，最少为有影响力。 

下表中的基于软件的重置选项在所有 Windows 10 版本 1809 MBB 设备上可用，并可通过 OEM patners 禁用或配置。

| 重置序列 | 重置类型    | 重置机制 |
| ---------------|-------------- | --------------- |
| 1              | 仅软件 | 停用和激活 PDP 上下文 |
| 2              | 仅软件 | 切换飞行模式 (APM) 开/关 |
| 3              | 仅软件  | 在即插即用 (PnP) 级别启用/禁用设备 |

使用 MBB 设备/固件功能的 Oem 启用了以下基于设备的重置选项。 

| 重置序列 | 重置类型   | 重置机制 |
| -------------- |------------- | --------------- |
| 4              | 基于设备 | 功能级别设备重置 (FLDR)  |
| 5              | 基于设备 | 平台级别设备重置 (PLDR)  |

恢复顺序已更改，在某些情况下，对于某些类型的故障，某些情况下会绕过某些类型的重置机制。 例如，如果在切换飞行模式时出现命令超时，则操作系统不会切换飞行模式来修复它。 如果 MBB 设备不响应任何 MBIM 命令，则操作系统会直接与基于设备的重置机制联系。

对于启用 MBIM 函数的 UDE 客户端驱动程序，Windows 10 1809 版包含一个新的 API，可用于在 UDECx 客户端驱动程序检测到错误时请求重置。 以下部分介绍了这些新的基于设备的重置 mechanims，包括 PCI 的 FLDR、PLDR 和 UDECx reset。

## <a name="device-based-resets"></a>基于设备的重置

### <a name="function-level-device-reset-fldr"></a>功能级设备重置 (FLDR) 

在系统影响方面，函数级设备重置是基于设备的最浅重置。 它发生在设备内部，并对其他设备不可见，在整个重置过程中，该设备保持连接到总线，并返回到有效状态 (换言之，在该过程之后) 初始状态。 这可以由总线驱动程序或固件提供。 如果总线规范定义满足要求的带内重置机制，则总线驱动程序实现 FLDR 处理程序。 固件编写器可能会使用其自己的 FLDR 实现（如重置线路或电源切换）替代总线定义的 FLDR，但仍遵循 FLDR 的要求。 

### <a name="platform-level-device-reset-pldr"></a>平台级别设备重置 (PLDR)   

对于不能使用 FLDR 或作为 FLDR 的最后滑雪场补充的情况，平台级设备重置。 这种重置机制导致在电源周期中将设备报告为缺少总线 (，例如) 或影响多台设备 (如共享电源导轨或设备) 中的重置线路。 在 ACPI 表中指定了 reset 方法，该方法可能会实现为切换专用重置线路或对 D3 电源资源进行重启。 执行 PLDR 时，OS 会泪水并重建所有受影响设备的堆栈，以确保一切都从处于纯洁状态启动。

### <a name="reset-recovery-for-ude-devices"></a>重置 UDE 设备的恢复 

对于启用 MBIM 函数的 UDE 客户端驱动程序，Windows 10 1809 版包含一个 API，可用于在 UDECx 客户端驱动程序检测到错误时请求重置。 客户端驱动程序通过调用新方法 [**UdecxWdfDeviceNeedsReset**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)指定重置类型（如果支持) ，则指定它希望 UDECx 尝试设备 (）。 这些重置类型包括 **PlatformLevelDeviceReset** 和 **FunctionLevelDeviceReset** ，它们是 [**UDECX_WDF_DEVICE_RESET_TYPE**](/windows-hardware/drivers/ddi/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type) 枚举的值。 启动重置后，UDECx 将调用驱动程序的 [*EVT_UDECX_WDF_DEVICE_RESET*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset) 回调函数，并确保在此过程中不会调用任何其他回调。 客户端驱动程序应执行任何重置相关操作（如释放任何资源），然后通过调用 [**UdecxWdfDeviceResetComplete**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)来完成信号重置。

以下流程图说明了 UDE 设备重置过程。

![UDECx 客户端驱动程序的重置恢复流的流](images/mb-self-healing-udecx-reset.png "UDECx 客户端驱动程序的重置恢复的调用流。")


## <a name="rnr-triggers"></a>RnR 触发器
WWAN 服务将可操作的故障组织到 RnR 触发器中：
1. 连接错误
2. 无线电状态设置/查询失败/超时
3. 连续 OID 请求超时
4. 初始化失败

### <a name="rnr-trigger-1---bad-connectivity"></a>RnR 触发器 #1-不良连接
* 连接错误
* Internet 连接受限
* 失去 Internet 连接
* 路由未正确接收
* 无法访问路由
* 失效的网关
* DNS 查询失败
    
WCM 根据 (NCSI 等 ) 的各种源进行检测。

WCM 发布 WNF_WCM_INTERFACE_CONNECTION_STATE。
```
struct WCM_WNF_INTERFACE_CONNECTION_STATE_INFO
{
    GUID InterfaceGuid;
    WCM_MEDIA_TYPE MediaType = wcm_media_unknown;
    // ConnectionState is one of the WCM_WNF_INTERFACE_CONNECTIVITY_STATE_* values
    DWORD ConnectionState = 0;
    // TimeInBadStateMs tracks how long a connection is in a Bad state
    // It will reset back to zero when in a good state
    DWORD TimeInBadStateMs = 0;
    // ConnectivityTriggers is a bitmask of WCM_WNF_INTERFACE_CONNECTIVITY_TRIGGER_* flags
    DWORD ConnectivityTriggers = 0; 
    // fWasConnectedGood will be TRUE if a connection is ever in a good state over the lifetime of an L2 connection
    // Once it is set to TRUE, it will never go FALSE until the interface disconnects
    BOOLEAN fWasConnectedGood = FALSE;
    // When processing the WNF, walk the array of WCM_WNF_INTERFACE_CONNECTION_STATE_INFO structs
    // until you reach the struct with afLastArrayValues == TRUE
    BOOLEAN fLastArrayValue = TRUE;
};
```
恢复过程：
* 将 PDP 上下文重置为三次 (参阅 FSM 转换关系图) 
* 切换 APM 一次
* PnP 禁用和启用 MBB 设备一次
* 如果受支持，则调用一次 FLDR
* 如果受支持，则调用一次 PLDR

当 L3 连接良好时，进程将立即停止。

结果验证： L3 连接良好。
 
### <a name="rnr-trigger-2----radio-state-setquery-failure-or-time-out"></a>RnR 触发器 #2-无线电状态集/查询失败或超时
* 设置或查询无线电状态没有响应或失败响应。
* OID_WWAN_RADIO_STATE 集或查询请求。
* 永远不会发生。
* 一旦发生，操作系统和调制解调器可能会处于不一致的状态。
* 表明调制解调器)  (的严重问题。
* CWwanExecutor 检测到它，并将其内部报告给 CWwanResetRecovery。

恢复过程：
* 如果支持，则调用 PLDR
* 否则，调用 PnP 禁用/启用

结果验证：发送 OID_WWAN_RADIO_STATE 查询并验证响应。

### <a name="rnr-trigger-3---time-out-of-consecutive-oid-requests"></a>RnR trigger #3-连续 OID 请求超时
* TXM 会对所有未完成的 OID 请求并预期每个请求的响应。
* 如果 "可配置" 的连续 OID 请求数没有及时接收到响应，则 TXM 会检测到它，并将其内部报告给 CWwanResetRecovery。
* 可以将 Oid 分组为高/中/低延迟组：
    * 与 MO 无交互的 OID 请求会降低延迟。
    * 导致与 MO 交互的 OID 请求将有中等滞后时间。
    * OID_WWAN_CONNECT 激活/停用请求：约180秒。

恢复过程：
* 如果支持，则调用 PLDR
* 否则，调用 PnP 禁用/启用

结果验证：发送 OID_WWAN_RADIO_STATE 查询并验证响应。

### <a name="rnr-trigger-4---initialization-failures"></a>RnR 触发器 #4 初始化失败
* 设备 cap 或设备 capsEx 查询在达到 MB 设备时进行初始化的超时
* CWwanManager 检测并处理它

恢复过程：
- 如果支持，则调用 PLDR
- 否则，调用 PnP 禁用/启用

结果验证：无

PLDR 或 PnP 禁用/启用后，设备离开，然后重新到达。 到达时进行初始化，如下所示。

### <a name="primary-flows"></a>主流程
#### <a name="rnr-for-bad-connectivity"></a>RnR 进行不良连接
![RnR 进行不良连接](images\RnR_bad_connectivity.png?raw=true "RNR_bad_connectivity")
#### <a name="pldr-for-radio-power-set-failure"></a>无线电电源设置失败的 PLDR
![无线电电源设置失败的 PLDR](images\PLDR_radio_power_set_failure.png?raw=true "PLDR_radio_power_set_failure")
#### <a name="pnp-disableenable-for-radio-state-set-failure"></a>为无线电状态设置失败启用 PnP 禁用/启用
![无线电状态设置失败的 PnP](images\PnP_radio_state_set_failure.png?raw=true "PnP_radio_state_set_failure")
#### <a name="pldr-for-time-outs-of-consecutive-oid-requests"></a>用于连续 OID 请求的超时的 PLDR 
![PLDR 连续 OID 请求超时](images\PLDR_timeouts_consecutive_OID_requests.png?raw=true "PLDR_timeouts_consecutive_OID_requests")
#### <a name="pnp-disableenable-for-time-outs-of-consecutive-oid-requests"></a>PnP 禁用/启用用于连续 OID 请求的超时时间 
![超时连续 OID 请求的 PnP](images\PnP_timeouts_consecutive_OID_requests.png?raw=true "PnP_timeouts_consecutive_OID_requests")
#### <a name="pldr-for-initialization-failure"></a>PLDR 初始化失败
![PLDR 初始化失败](images\PLDR_initialization_failure.png?raw=true "PLDR_initialization_failure")
#### <a name="pnp-disableenable-for-initialization-failure"></a>用于初始化失败的 PnP 禁用/启用
![初始化失败](images\PnP_initialization_failure.png?raw=true "PnP_initialization_failure")


## <a name="requirements-for-mb-device-based-reset-and-recovery"></a>基于设备的重置和恢复的要求

### <a name="requirements-for-fldr"></a>FLDR 的要求

若要支持设备上的 FLDR，必须在设备 () 范围内 `_RST` 定义方法。 执行时，该方法必须仅重置该设备，而不应触摸另一台设备。 设备还必须在总线上保持连接状态。 

```cpp
Device(PCI0)  
{  
Device(USB0)  
{  
    Name(_ADR, 0x1d0000)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Method(_RST, 0x0, NotSerialized)  
    {  
            //  
            // Perform reset of the USB0 device  
            //  
    } 
} 
} 
```

### <a name="requirements-for-pldr"></a>PLDR 的要求

在 PLDR 中，受其他设备重置影响的设备表示为 "共享" `PowerResource` 以进行重置。 设备声明它们对的依赖项 `PowerResource` 以重置，并 `PowerResource` 实现 `_RST` 方法。 

```cpp
Device(PCI0)  
{  
PowerResource(URST, 0x5, 0x0)  
{  
    //  
    // Dummy _ON and _OFF methods. All power resources must have these  
    // two defined.  
    // Method(_ON, 0x0, NotSerialized)  
    {  
    }  
    Method(_OFF, 0x0, NotSerialized)  
    {  
    }  
    Method(_RST, 0x0, NotSerialized)  
    {  
            //  
            // Perform reset of the USB0 and USB1 devices  
            //  
    } 
}  
Device(USB0)  
{  
    Name(_ADR, 0x1d0000)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Name(_PRR, Package(0x1) { ^URST })  
}  
Device(USB1)  
{  
    Name(_ADR, 0x1d0001)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Name(_PRR, Package(0x1) { ^URST })  
} 
} 
```

或者，可以通过将设备置于 D3Cold 电源状态并返回到 D0 来实现 PLDR，实质上是重新启动设备。 在这种情况下， `_PR3` 在设备范围内声明足以支持 PLDR。 `_PR3`如果设备范围内未引用任何设备，ACPI 将使用来确定设备之间的重置依赖项 `_PRR` 。 有关详细信息，请参阅 [重置和恢复设备](../kernel/resetting-and-recovering-a-device.md)。 

## <a name="sample-log"></a>示例日志
```
NTS]WWAN Service event: [Info] WwanTimerWrapper::StartTimer:  Timer (ID = 0) Start Completed
[0]0E98.34E4::11/27/2019-05:37:55.622 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] WwanTxmEvaluateArmTimer: TXM timer armed for 60 seconds Interface: {{8a664721-db25-4157-8395-5d21e0560fa4}}
[0]0E98.34E4::11/27/2019-05:37:55.622 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] _sendReq: ASYNC OID (pTx->handle: 00000000000000B0 Code: 1) sent
[0]0E98.34E4::11/27/2019-05:37:55.622 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanExecutor::RegWriteStoredRadioState: Try to set the subkey to 0x0 for ArrivalRadioState Interface: {{8a664721-db25-4157-8395-5d21e0560fa4}}
[0]0E98.34E4::11/27/2019-05:37:55.623 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanResetRecovery::EvaluateAndTryHighImpactRnRMethod:  Attempted to turn off radio via MBB (reqId 0x10c): request ID 0x1 prev stage 0 APMToggling 0; PnPDisabling 0; PLDR 0; FLDR 0 Interface: {{8a664721-db25-4157-8395-5d21e0560fa4}}
[0]0E98.34E4::11/27/2019-05:37:55.623 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] WwanTimerWrapper::StartTimer:  Timer (ID = 6) Start Completed
[0]0E98.34E4::11/27/2019-05:37:55.623 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanResetRecovery::fsmEventHandler:  exit with state: 7, event: 4, RnR stage: 2 Potent RnR: 0 Interface: {{8a664721-db25-4157-8395-5d21e0560fa4}}
```

## <a name="related-links"></a>相关链接

[MB 挂起检测](mb-hang-detection.md)

[**UDECX_WDF_DEVICE_RESET_TYPE**](/windows-hardware/drivers/ddi/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)

[**UdecxWdfDeviceNeedsReset**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

[*EVT_UDECX_WDF_DEVICE_RESET*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)

[**UdecxWdfDeviceResetComplete**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)
