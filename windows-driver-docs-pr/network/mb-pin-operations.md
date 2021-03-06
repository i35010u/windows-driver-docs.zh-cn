---
title: MB PIN 操作
description: MB PIN 操作
ms.date: 03/05/2021
ms.localizationpriority: medium
ms.openlocfilehash: 0d9ba071ee469ca21af9243d270a0985237b3059
ms.sourcegitcommit: 6c8f5e213c58e941547cc77abb67e55134b9598f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102255185"
---
# <a name="mb-pin-operations"></a>MB PIN 操作

## <a name="overview"></a>概述

本主题介绍与访问控制存储在 MB 设备内存或订阅服务器标识模块 (SIM) 卡上的订阅信息相关的操作。 这包括启用、禁用或更改个人识别码 (PIN) ，以及通过 PIN 或个人解锁密钥 (PUK) 解锁。 

## <a name="architectureflows"></a>体系结构/流
启用/禁用/解锁/更改 PIN 的用户操作

![固定操作流程图](images/pinActions.png)

&nbsp;

PIN1/PUK1 状态的移动用户 UX 查询

![Query PIN1/PUK1 流程图](images/pinQuery.png)

&nbsp;

从休眠状态恢复后自动解锁

![从休眠流程图恢复后自动解锁](images/auto-unlock-pin-hibernation.png)

## <a name="mbim_cid_ms_pin_ex"></a>MBIM_CID_MS_PIN_EX

此处描述了此 CID： [MBIM_CID_MS_PIN_EX](/windows-hardware/drivers/network/mb-uicc-application-and-file-system-access#mbim_cid_ms_pin_ex)

## <a name="mbim_cid_pin_list"></a>MBIM_CID_PIN_LIST

### <a name="description"></a>描述

此命令将返回一个列表，其中列出了 MB 设备支持的所有不同类型的个人标识号 (引脚) ，以及每个 PIN 类型的其他详细信息，例如 PIN 的长度 (最小和最大长度) 、PIN 格式和 PIN 输入模式 (启用/禁用/不可用) 。 此 CID 还指定该函数支持的每个 PIN 的当前模式。
函数必须报告其支持的所有 Pin。 但是，对于多模式设备，PIN1 只能报告一次。

报告为 PIN1 的 PIN 必须符合 PIN1 准则：对于基于 CDMA 的设备，这是一个提供开机验证或识别功能的 PIN，而对于基于 GSM 的设备，这是一个订户标识模块 (SIM) PIN。

当 ready 状态更改为 MBIMSubscriberReadyStateInitialized 或就绪状态为 MBIMSubscriberReadyStateDeviceLocked (PIN 锁定) 时，函数必须能够返回此信息。 函数还应尽可能将此信息返回到其他就绪状态。

#### <a name="query-only"></a>仅查询

查询消息的 InformationBuffer 为空。 MBIM_COMMAND_DONE 的 InformationBuffer 包含 MBIM_PIN_LIST_INFO。

### <a name="parameters"></a>参数

|   | 设置 | 查询 | 通知 |
|---|---|---|---|
| **命令**  | 不可用 | 空              | 不可用 |
| **响应** | 不可用 | MBIM_PIN_LIST_INFO | 不可用 |

### <a name="data-structures"></a>数据结构

#### <a name="mbim_pin_mode"></a>MBIM_PIN_MODE

| 类型 | 值 |
|---|---|
| MBIMPinModeNotSupported | 0 |
| MBIMPinModeEnabled      | 1 |
| MBIMPinModeDisabled     | 2 |

#### <a name="mbim_pin_format"></a>MBIM_PIN_FORMAT

| 类型 | 值 |
|---|---|
| MBIMPinFormatUnknown      | 0 |
| MBIMPinFormatNumeric      | 1 |
| MBIMPinFormatAlphaNumeric | 2 |

#### <a name="mbim_pin_desc"></a>MBIM_PIN_DESC

| Offset | 大小 | 字段 | 类型 | 描述 | 
|---|---|---|---|---|
| 0 | 4 | PinMode      | MBIM_PIN_MODE | 请参阅上表 [MBIM_PIN_MODE](#mbim_pin_mode)。 这会显示锁定是否已启用。 它不显示锁定状态是锁定还是解除锁定。 |
| 4 | 4 | PinFormat    | MBIM_PIN_FORMAT | 请参阅上表 [MBIM_PIN_FORMAT](#mbim_pin_format)。 |
| 8 | 4 | PinLengthMin | UINT32 | PIN 中的最小字符数。 设备不应指定大于16的值。 如果 PIN 长度不可用，则设备应指定0xffffffff。 |
| 12| 4 | PinLengthMax | UINT32 | PIN 中的最大字符数。 设备不应指定大于16的值。 如果 PIN 长度不可用，则设备应指定0xffffffff。 |


### <a name="query"></a>查询

InformationBuffer 应为 **null** ，而 InformationBufferLength 应为 **零**。

### <a name="response"></a>响应

应在 InformationBuffer 中使用以下结构：

#### <a name="mbim_pin_list_info"></a>MBIM_PIN_LIST_INFO

| Offset | 大小 | 字段 | 类型 | 描述 | 
|---|---|---|---|---|
| 0 | 16 | PinDescPin1                | MBIM_PIN_DESC | 描述 PIN1 的 MBIM_PIN_DESC 结构。 对于 GSMbased 设备，这是 (SIM) PIN 的订户标识模块。 对于基于 CDMA 的设备，开机设备锁定将报告为 PIN1。 |
| 16 | 16 | PinDescPin2               | MBIM_PIN_DESC | 描述 PIN2 的 MBIM_PIN_DESC 结构。 这是一个用于保护某些 SIM 功能的 SIM PIN2。 |
| 32 | 16 | PinDescDeviceSimPin       | MBIM_PIN_DESC | 描述设备到 SIM 卡 PIN 的 MBIM_PIN_DESC 结构。 这是将设备锁定到特定 SIM 的 PIN。 |
| 48 | 16 | PinDescDeviceFirstSimPin  | MBIM_PIN_DESC | 描述设备到的第一个-SIM 卡 PIN 的 MBIM_PIN_DESC 结构。 这是将设备锁定为第一个插入的 SIM 的 PIN。 |
| 64 | 16 | PinDescNetworkPin         | MBIM_PIN_DESC | 描述网络个性化设置 PIN 的 MBIM_PIN_DESC 结构。 这是允许将设备个性化到网络的 PIN。 有关此 PIN 类型的详细信息，请参阅3GPP 规范22.022。 |
| 80 | 16 | PinDescNetworkSubsetPin   | MBIM_PIN_DESC | 描述网络子集个性化设置 PIN 的 MBIM_PIN_DESC 结构。 这是允许将设备个性化到网络子集的 PIN。 有关此 PIN 类型的详细信息，请参阅3GPP 规范22.022。 |
| 96 | 16 | PinDescServiceProviderPin | MBIM_PIN_DESC | MBIM_PIN_DESC 结构，用于描述服务提供程序 (SP) 个性化设置 PIN。 这是允许将设备个性化到服务提供商的 PIN。 有关此 PIN 类型的详细信息，请参阅3GPP 规范22.022。 |
| 112 | 16 | PinDescCorporatePin      | MBIM_PIN_DESC | 描述公司个性化设置 PIN 的 MBIM_PIN_DESC 结构。 这是允许将设备个性化到特定公司的 PIN。 有关此 PIN 类型的详细信息，请参阅3GPP 规范22.022。 |
| 128 | 16 | PinDescSubsidyLock       | MBIM_PIN_DESC | 描述 subsidy 解锁 PIN 的 MBIM_PIN_DESC 结构。 这是一种允许设备被限制为在特定网络上运行的 PIN。 有关此 PIN 类型的详细信息，请参阅3GPP 规范22.022。 |
| 144 | 16 | PinDescCustom            | MBIM_PIN_DESC | 描述自定义 PIN 的 MBIM_PIN_DESC 结构。 这是自定义供应商定义的 PIN 类型。 以上列表中不包括此项。 |

### <a name="status-codes"></a>状态代码

状态代码 | 说明
---|---
MBIM_STATUS_PIN_REQUIRED | PIN 列表操作失败，因为必须先输入 PIN，然后才能继续执行此操作。

## <a name="testing"></a>测试

以下测试将作为 **TestPin** HLK 测试列表的一部分运行：

测试名称 | 描述
---|---
PinListQueryRadioOn | 此测试尝试在上使用广播的 pin 列表查询。
PinListQueryRadioOff | 此测试尝试使用无线电关闭 pin 列表查询。
NoPinSupport | 此测试验证不支持 PIN1 的设备。
PinExSetEnableDisableWithValidPin | 此测试使用有效的 pin 来启用和禁用 PIN1。
PinExSetDisableIncorrectPinWithValidLength | 此测试尝试使用具有有效长度的错误 pin 来启用 PIN1。
PukEnableDisableThroughIncorrectPinExDisable | 此测试通过多次输入错误的 PIN1 来启用 PUK1，并禁用 PUK1。
PinExSetChangeWithBothInvalidAndValidPin | 此测试启用 PIN1，立即更改 PIN 并禁用它。
RebootTestMachineToPutPinIntoLockState | 此测试将重新启动设备，使调制解调器进入锁定状态并提示输入有效的 PIN 条目。
PinExSetEnterWithValidPin | 此测试验证设备是否处于锁定状态以请求 PIN 代码条目。


**TestPowerStates** HLK 测试列表还包含一个相关测试-- **SimPinUnlockAfterHibernate**。


## <a name="log-analysis"></a>日志分析

### <a name="sample-logs"></a>示例日志：

自动解锁：
```
462678 [0]0F3C.1280::2020-05-05 13:03:46.378805100 [Microsoft-Windows-WWAN-SVC-EVENTS][Request=0x53] Received PinInfo, status=WWAN_STATUS_SUCCESS , Type=WwanPinTypePin1  State=WwanPinStateEnter  Attempts=3, miniport={7971731f-33f9-4f1a-9718-087c12e64c5d} 
462753 [7]0F3C.2A6C::2020-05-05 13:03:46.379718400 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::maybeUnlockPin:  Attempting auto-PIN-unlock. Interface: {{7971731f-33f9-4f1a-9718-087c12e64c5d}} 
462809 [7]0F3C.2A6C::2020-05-05 13:03:46.380157500 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Error] CWwanPinSM::maybeUnlockPin: Attempt to auto-unlock PIN succeeded 
```

设置 Pin (WwanPinTypePin1) ：
```
546408 [3]0F3C.1240::2020/05/02-09:18:09.178460200 [Microsoft-Windows-WWAN-SVC-EVENTS][Request=0x6C] Sent SET PinAction, Type=2(WwanPinTypePin1), Operation=0(WwanPinOperationEnter), miniport={7971731f-33f9-4f1a-9718-087c12e64c5d}, ErrorCode=3407873(WIN=The request will be completed later by NDIS status indication.)
546425 [1]3DB0.12EC::2020/05/02-09:18:09.178564700 [Microsoft.Windows.CellCore.MBBSettingsUX]{"meta":{"provider":"Microsoft.Windows.CellCore.MBBSettingsUX","event":"MBCategory::_SetPinAction. WwanSetInterface succeeded","time":"2020-05-02T16:18:09.1785647Z","cpu":1,"pid":15792,"tid":4844,"channel":11,"level":4}}
546644 [2]0F3C.39E4::2020/05/02-09:18:09.426362600 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::processPinActionResponse: SetPin rsp rcvd (result:0x0) PIN Info (state:1, type:3, attemptsRemaining:3) IsPin1Blocked 0
546645 [2]0F3C.39E4::2020/05/02-09:18:09.426364800 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::maybeCapturePin: Capturing PIN for PIN ENTER/ENABLE operation Interface: {{7971731f-33f9-4f1a-9718-087c12e64c5d}}
546688 [7]3B64.2A80::2020/05/02-09:18:09.426727000 [MbaeApiLogging]{"NotificationCode":"WwanMsmEventTypePinActionComplete: Success","AdapterID":"{7971731f-33f9-4f1a-9718-087c12e64c5d}","NotificationSize":24,"meta":{"provider":"MbaeApiLogging","event":"CWwanTranslator::ProcessWwanNotification","time":"2020-05-02T16:18:09.4267270Z","cpu":7,"pid":15204,"tid":10880,"channel":11,"level":5}}
546702 [0]3B64.242C::2020/05/02-09:18:09.426762000 [Microsoft.Windows.CellCore.MBBSettingsUX]{"meta":{"provider":"Microsoft.Windows.CellCore.MBBSettingsUX","event":"MBMediaManager::ProcessWwanNotification WwanMsmEventTypePinActionComplete","time":"2020-05-02T16:18:09.4267620Z","cpu":0,"pid":15204,"tid":9260,"channel":11,"level":4}}
546710 [7]0F3C.1208::2020/05/02-09:18:09.426809700 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] _PublishSebNotification: Event Source=WwanNotificationSourceMsm, Code=WwanMsmEventTypePinActionComplete
547064 [2]3DB0.1194::2020/05/02-09:18:09.427921200 [MbaeApiLogging]{"NotificationCode":"WwanMsmEventTypePinActionComplete: Success","AdapterID":"{7971731f-33f9-4f1a-9718-087c12e64c5d}","NotificationSize":24,"meta":{"provider":"MbaeApiLogging","event":"CWwanTranslator::ProcessWwanNotification","time":"2020-05-02T16:18:09.4279212Z","cpu":2,"pid":15792,"tid":4500,"channel":11,"level":5}}
547106 [2]3DB0.0B38::2020/05/02-09:18:09.428040100 [Microsoft.Windows.CellCore.MBBSettingsUX]{"meta":{"provider":"Microsoft.Windows.CellCore.MBBSettingsUX","event":"MBMediaManager::ProcessWwanNotification WwanMsmEventTypePinActionComplete","time":"2020-05-02T16:18:09.4280401Z","cpu":2,"pid":15792,"tid":2872,"channel":11,"level":4}}
```

Pin 列表：
```
465632 [4]0F3C.47F4::2020-05-05 13:03:46.395488200 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: PIN1 (mode:1, format:1, pinlnmin:4, pinlnmax:8) 
465633 [4]0F3C.47F4::2020-05-05 13:03:46.395489800 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: PIN2 (mode:1, format:1, pinlnmin:4, pinlnmax:8) 
465634 [4]0F3C.47F4::2020-05-05 13:03:46.395491400 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: DEVSIMPIN (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
465635 [4]0F3C.47F4::2020-05-05 13:03:46.395492800 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: DEVFIRSTSIMPIN (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
465636 [4]0F3C.47F4::2020-05-05 13:03:46.395494200 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: NWPIN (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
465637 [4]0F3C.47F4::2020-05-05 13:03:46.395495800 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: NWSUBSETPIN (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
465641 [5]0F3C.47F4::2020-05-05 13:03:46.395510100 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: SVCPROVIDERPIN (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
465643 [5]0F3C.47F4::2020-05-05 13:03:46.395513700 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: CORPORATEPIN (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
465644 [5]0F3C.47F4::2020-05-05 13:03:46.395515200 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanPinSM::tracePinDesc: SUBSIDYLOCK (mode:0, format:0, pinlnmin:0, pinlnmax:0) 
```

## <a name="winrt-api"></a>WinRT API
[MobileBroadbandPin 类](/uwp/api/windows.networking.networkoperators.mobilebroadbandpin?view=winrt-18362&preserve-view=true)

## <a name="see-also"></a>另请参阅

[OID_WWAN_PIN_EX2](/windows-hardware/drivers/network/oid-wwan-pin-ex2)

[OID_WWAN_PIN_LIST](/windows-hardware/drivers/network/oid-wwan-pin-list)

[MB UICC 应用程序和文件系统访问权限](/windows-hardware/drivers/network/mb-uicc-application-and-file-system-access)

有关 PIN 操作的其他信息，请参阅 [OID \_ WWAN \_ PIN](oid-wwan-pin.md)。
