---
title: MB 无线电状态
description: 了解蜂窝广播状态的体系结构和流，以及如何对其进行测试和调试。
keywords: 飞行模式，移动电话无线电状态，MB 无线电电源状态
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 9c50f0d03c26424b16cfa40d58ae2e628167ee80
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719476"
---
# <a name="mb-radio-state"></a>MB 无线电状态

## <a name="overview"></a>概述

本主题介绍了用于设置和读取 MB 设备的无线电电源状态 (s) 的操作。 如果适当的交换机存在) ，可以通过软件 (飞行模式) 或硬件 (控制这些状态。 本主题说明如何控制无线电电源状态，如何测试无线电电源状态功能，以及如何调查无线电功率状态问题。 

### <a name="terminology"></a>术语

*系统无线电状态* -系统无线电状态为系统范围内的状态。 它是飞行模式状态最明显的指示器。 系统无线电状态由无线电管理服务 (RmSvc) 管理。

*无线电管理器* -RmSvc 在系统中循环访问多个 RadioManagers (MediaManagers) ，如 WlanRadioManager、BlueTooth 和 WwanRadioManager。 WwanRadioManager () 在 RmSvc.dll 中承载，并管理该广播逻辑的 wwan 端。 WwanRadioManager 使用 WWAN 服务 (WwanSvc) RPC 来执行以下操作： 
1. 查询并设置手机网络广播。
1. 控制飞行模式之前和之后的流。

*单选钮* -每个 RadioManager 可以包含多个单选钮。 例如，如果系统中有两个移动电话调制解调器，WwanRadioManager 可以有两个单选钮。 每个广播实例都是抽象对象，应映射到一个硬件收音机模块。 在大多数情况下，每个广播实例都映射到一个蜂窝调制解调器。

### <a name="relevant-services-and-drivers"></a>相关的服务和驱动程序

*RmSvc.dll* -管理系统范围的无线电事件，如飞行模式。 它还托管所有收音机管理器，包括 WwanRadioManager。

*WwanSvc.dll* -移动电话调制解调器由 WwanSvc 管理。 因此，通过 WwanSvc 发出 OID/CID)  (命令。 RmSvc 或其他组件 (UI 的外部请求) 通过 WwanSvc RPC 来查询或设置手机网络无线电状态。

*MbbCx.sys* -用于管理设备电源状态的内核模式驱动程序，特别是 D0 和 Dx 转换之间。 在某些系统设置上，允许设备转换为 Dx 状态，仅在需要时恢复为 D0。 MbbCx.sys 在 D0 和 Dx 之前管理无线电状态恢复的逻辑和控制。

## <a name="architectureflows"></a>体系结构/流

### <a name="radio-control-from-wwansvc-to-modem-hardware"></a>从 WwanSvc 到调制解调器硬件的无线电控制
![从 WwanSvc 到调制解调器硬件流程图的无线电控制](images/airplane-mode-wwansvc-to-modemhw.png)

### <a name="set-radio-via-wwansvc-api"></a>通过 WwanSvc API 设置收音机
![通过 WwanSvc API 流程图设置收音机](images/airplane-mode-wwansvcapi-set-radio.png)

### <a name="initial-radio-state-upon-device-arrival"></a>设备到达时的初始无线电状态
![设备到达流程图时的初始无线电状态](images/airplane-mode-arrival-state.png)

## <a name="mbim_cid_radio_state"></a>MBIM_CID_RADIO_STATE

如上图所示，在飞行模式操作中使用的 CID **MBIM_CID_RADIO_STATE**。 此 CID 设置或返回有关 MB 设备无线电电源状态的信息。

### <a name="query"></a>查询
不使用 MBIM_COMMAND_MSG 上的 InformationBuffer。 MBIM_RADIO_STATE_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

### <a name="set"></a>设置
MBIM_COMMAND_MSG 上的 InformationBuffer 包含 MBIM_SET_RADIO_STATE。 MBIM_RADIO_STATE_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

### <a name="unsolicited-event"></a>主动事件
事件 InformationBuffer 包含 MBIM_RADIO_STATE_INFO 结构。

### <a name="parameters"></a>parameters

|   | 设置 | 查询 | 通知 |
|---|---|---|---|
| **命令**  | MBIM_SET_RADIO_STATE  | 空                 | 不适用                   |
| **响应** | MBIM_RADIO_STATE_INFO | MBIM_RADIO_STATE_INFO | MBIM_RADIO_STATE_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="set"></a>设置

| Offset | 大小 | 字段 | 类型 | 说明 | 
|---|---|---|---|---|
| 0 | 4 | RadioState | MBIM_RADIO_SWITCH_STATE | 设置软件控制的无线电状态。 请参阅下表。 |

**MBIM_RADIO_SWITCH_STATE**

| 类型        | 值 |
|--------------|-------|
| MBIMRadioOff | 0     |
| MBIMRadioOn  | 1     |

#### <a name="query"></a>查询
 InformationBuffer 将为 **null** ，InformationBufferLength 将为 **零**。

#### <a name="response"></a>响应
**MBIM_RADIO_STATE_INFO**

| Offset | 大小 | 字段 | 类型 | 说明 | 
|---|---|---|---|---|
| 0 | 4 | HwRadioState | MBIM_RADIO_SWITCH_STATE | W_DISABLE 开关的状态。 如果设备没有 W_DISABLE 交换机，则该函数必须在此字段中返回 MBIMRadioOn。 |
| 4 | 4 | SwRadioState | MBIM_RADIO_SWITCH_STATE | 软件配置的无线电状态。 |

#### <a name="notification"></a>通知
请参阅上表中的 **MBIM_RADIO_STATE_INFO** 表。

#### <a name="status-codes"></a>状态代码
此 CID 只使用一般状态代码。


## <a name="testing"></a>测试

### <a name="cellular-radio-tests"></a>手机网络广播测试

| 函数名称   | 描述 |
|:----------------|:------------|
|CellularRadioWinrtTest::VerifyCellularModemExistence                 | 断言 winrt api 可以查询移动电话调制解调器和无线电状态                   |
|CellularRadioWinrtTest::VerifyCellularRadioToggle                    |Assert winrt api 可以在每个 wwan 适配器上切换广播状态                 |
|CellularRadioRecoveryTest::VerifyCellularRadioRecoveryToOnAfterAPM   |离开飞行模式时，断言蜂窝无线电状态将恢复到开启状态  |
|CellularRadioRecoveryTest::VerifyCellularRadioRecoveryToOffAfterAPM  |离开飞行模式时断言蜂窝无线电状态保持关闭状态           |
|CellularRadioRecoveryTest::VerifyCellularRadioAcrossSvcRestart       |断言蜂窝广播状态在 WwanSvc 重新启动时保持一致       |
|CellularRadioRecoveryTest::VerifyCellularRadioAcrossDevNodePnp       |断言蜂窝无线电状态在设备到达/删除时保持一致   |

**CellularRadioTest.dll** 包含这些测试。

## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试

请参阅 [安装 HLK 的步骤](https://microsoft.sharepoint.com/teams/HWKits/SitePages/HWLabKit/Manual%20Controller%20Installation.aspx)。

在 HLK Studio 中，连接到设备移动电话调制解调器驱动程序并运行以下测试：

- [**TestRadioStateSoftware**](/windows-hardware/test/hlk/testref/0aa9981a-e556-4338-a568-b17289dd9742) 
- [**TestRadioStateHardware**](/windows-hardware/test/hlk/testref/fa0bd189-b332-4651-8eda-e89866d2e2f1) 

或者，你可以通过 [**netsh-mbn**](/windows-server/networking/technologies/netsh/netsh-mbn)和 [**netsh-mbn**](mb-netsh-mbn-test.md)--运行 **TestRadioStateHardware** and **TestRadioStateSoftware** HLK testlist。
```
netsh mbn test feature=radio testpath="C:\data\test\bin" taefpath="C:\data\test\bin" param="AccessString=internet"
```
应已在运行 "netsh mbn test" 命令的目录中生成了显示 HLK 测试结果的两个文件： `TestRadioStateSoftware.htm` 和 `TestRadioStateHardware.htm` 。

可以使用以下说明收集和解码日志： [MB 收集日志](mb-collecting-logs.md)。

## <a name="analyzing-logs"></a>分析日志
### <a name="useful-keywordsregexp-for-filtering-traces"></a>用于筛选跟踪的有用关键字/regexp
    
- OID_WWAN_RADIO_STATE
- CWwanRadioInstance::OnSysRadioChange
- 输入 CUIRadioManager：： _SetSysRadio
- 正在离开 CUIRadioManager：： _SetSysRadio
- CWwanRadioInstance：： _SetSoftwareRadioState
- [WwanRadioManager]
- PostD0Entry: previousPowerState

- CWwanRadioManager：： OnSystemRadioStateChange (. ) + sysradiostate
- RMAPI (. ) + OnSystemRadioStateChange
- RMAPI (. ) + OnSystemRadioStateChange
- Wwan-svc (. ) + 广播
- mbbcx ( ) + 广播


### <a name="investigation-tips"></a>调查提示
- 确定这是全局 (系统范围) 还是仅限本地 (手机网络) 无线电问题。
-  (D0) 从无线电状态中区分设备电源状态。 它们是不同的概念，但却是高度相关的。
- 确保日志中包含必要的 ETW 提供程序。
- 使用方案缩小区域。 例如：
    - 如果它与飞行模式相关，请关注 RmSvc 和 WwanRadioManager。
    - 如果与 D0< >Dx、休眠或睡眠过渡相关，请关注 MBBCx。
    - 如果它与 UI 显示或状态不同步相关，请从 WwanSvc 开始。

## <a name="winrt-api"></a>WinRT API

### <a name="windowsdevicesradios"></a>Windows 无线设备
[Windows 无线收发](/uwp/api/windows.devices.radios) 器由控制所有收音机管理器和实例的无线电管理服务所有。 对于 WWAN 端，RadioKind 为 RadioKind：： MobileBroadband。
- GetRadiosAsync ( ) 
- SetStateAsync ( ) 
### <a name="windowsnetworkingnetworkoperators"></a>Windows.Networking.NetworkOperators
[Windows.networking.networkoperators 文档页](/uwp/api/windows.networking.networkoperators.mobilebroadbanddeviceinformation.currentradiostate)

此用于收音机管理的命名空间下唯一有用的实用工具是 MobileBroadbandDeviceInformation. CurrentRadioState。

## <a name="see-also"></a>另请参阅
[OID_WWAN_RADIO_STATE](./oid-wwan-radio-state.md)