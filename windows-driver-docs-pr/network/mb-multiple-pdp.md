---
title: 多个 PDP 上下文
description: scenraio 关于多个 PDP 上下文
keywords: MPDP，多个 PDP 上下文，额外的 PDP 上下文
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 081232e829252b131a8a9458ebf96c5c711a579f
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719474"
---
# <a name="multiple-pdp-contexts"></a>多个 PDP 上下文
## <a name="usage-scenarios"></a>使用方案

UWP mobile 宽带应用可以利用多个数据包数据协议 (PDP) 上下文来激活特殊的 PDP 上下文并指定路由数据流量的规则。 这些应用可以为特定目标或所有数据流量创建规则。

当移动宽带应用需要与网络交换数据时，它会检查可用网络和连接的网络。 如果移动宽带应用对于这些网络中的任何一种都有特殊规则，它将使用连接管理器 API 来打开特殊的 PDP 上下文。 如果此连接成功，则 PDP 上下文会为此连接提供路由规则并使用网络 Api 传输数据。 如果移动宽带应用收到 [**NetworkStatusChanged**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged) 事件，以查看是否有任何连接已更改以及是否需要为新连接打开 PDP 上下文，则应该重复此操作。
    
可以使用多个 PDP 上下文来启用高级服务。
- 区分计费–您可以使用多个 PDP 上下文改变数据或计费限制。 例如，Contoso 是为其客户开发了数据备份应用的移动运营商。 作为移动运营商，Contoso 可以创建多个 PDP 上下文，让高级订户免费使用该应用。 所有其他订阅者单独收费以使用它。

- 丰富的通信服务–由 GSM 关联创建的全球计划，提供丰富的通信服务，例如增强的电话簿、增强的消息传递和更多的调用。 丰富的通信服务跨移动运营商提供互操作性，并提供新的方法来使用现有资产和功能来提供高质量和创新性的通信服务。

- 赞助连接性–这允许用户使用特定类型的内容，而无需考虑其每月数据使用量。 内容提供商通过直接支付移动运营商、开展收入共享交易或进行一些其他业务安排，来补偿移动运营商。

- 个人热点–当使用连接作为个人热点时，某些移动运营商会对不同的费率收费。 可以使用多个 PDP 上下文区分这两者。

有关详细信息，请参阅 [使用多个 PDP 上下文开发应用](../mobilebroadband/developing-apps-using-multiple-pdp-contexts.md)。


## <a name="primary-flow"></a>主流程
### <a name="app-activates-additional-pdp-contexts"></a>应用会激活额外的 PDP 上下文：
![显示应用激活额外 PDP 上下文的流程图](images/App_activate_additional_PDP_contexts.PNG?raw=true "App_activate_additional_PDP_contexts")

### <a name="additional-netadapter-initialization"></a>其他 Get-netadapter 初始化
![其他 Get-netadapter 初始化](images/Additional_NetAdapter_Initialization.PNG?raw=true "Additional_NetAdapter_Initialization")


## <a name="decision-logic-in-wwansvc-for-additional-pdp-context-connections"></a>WwanSvc 中用于额外 PDP 上下文连接的决策逻辑

1. 仔细检查并更新 "为默认配置文件" 条件逻辑，因为它不再适用。
1. WCM 不应再使用默认配置文件的 *cost* 属性。
1. 如果新的额外 pdp 上下文 APN 请求与默认 internet APN 一致，请断开当前额外的 PDP 上下文。

![WWANSVC 中用于连接额外的 PDP 上下文连接的决策逻辑](images/design_wwansvc_additional_pdp_contexts.png?raw=true "design_wwansvc_additional_pdp_contexts")


## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试
请参阅 [安装 HLK 的步骤](https://microsoft.sharepoint.com/teams/HWKits/SitePages/HWLabKit/Manual%20Controller%20Installation.aspx)。 

在 HLK Studio 中，连接到设备移动电话调制解调器驱动程序并运行测试： [Win6_4. MB。GSM.TestMPDP](/windows-hardware/test/hlk/testref/08497822-4355-478b-9cba-0c0c7b663953)。

## <a name="mb-multiple-pdp-context-troubleshooting-guide"></a>MB 多个 PDP 上下文疑难解答指南

1. 可以使用以下说明收集和解码日志： [MB 收集日志](mb-collecting-logs.md)
1. 打开[TextAnalysisTool](mb-analyzing-logs.md)中的 .txt 文件。
1. 加载 [Bacis 连接筛选器](mb-basic-connectivity-tat.md)

### <a name="sample-log"></a>示例日志
```
e 04-01 12:39:12.798 P4912 T8420 Microsoft-Windows-WWAN-NDISUIO-EVENTS WWAN NDISUIO Event: OID request sent to the driver                                                   0                    Info Microsoft-Windows-WWAN-NDISUIO-EVENTS
e 04-01 12:39:12.798 P4912 T8420 Windows Mobile Broadband Class Driver Event Provider [1] Miniport Request called Request=0xFFFFE3862EFF4A80, OID=0xE010149, OID name=OID_WWAN_MPDP RequestId=0x10F, RequestHandle=0x0, Type=1, InformationLength=32 0                    Info Windows Mobile Broadband Class Driver Event Provider
w 04-01 12:39:12.798 P4912 T8420 mbbcx         [ReqMgr][ReqId=0x04ad] Request created for OID_WWAN_MPDP [RequestContext=0xFFFFE386247597F0 OidRequest=0xFFFFE3862EFF4A80] SET=0x00000001(TRUE) MbbReqMgrCreateRequest requestmanager_cpp702 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.798 P4912 T8420 mbbcx         [ReqFsm][ReqId=0x04ad] Transition: MbbRequestStateReady -> MbbRequestStateDispatching event=MbbRequestEventDispatch MbbReqMgrQueueEvent  requestmanager_cpp1002 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.798 P4912 T8420 mbbcx         [ReqMgr][Timer] MbbTimerTypeRequest already armed at 3fc53, not re-arming                            MbbReqMgrTimerArm    requestmanager_cpp1269 TRACE_LEVEL_WARNING
w 04-01 12:39:12.798 P4912 T8420 mbbcx         [ReqMgr][ReqId=0x04ad], IsPoweredRequest [0x00000001(TRUE)], IsSerialized[0x00000001(TRUE)], IsQueueEmpty[0x00000001(TRUE)], DispatchRequest [0x00000000(FALSE)] MbbReqFsmDispatching requestmanager_cpp1522 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.798 P4912 T8420 mbbcx         MbxDevice::QueuePoweredRequest: WDFREQUEST (0x00001C79D4B06DB8) is sent                              MbxDevice::QueuePoweredRequest mbxdevice_cpp1339 TRACE_LEVEL_INFORMATION
e 04-01 12:39:12.798 P4912 T8420 Windows Mobile Broadband Class Driver Event Provider [1] Miniport REQUEST exited with status=The operation that was requested is pending completion., Request=0xFFFFE3862EFF4A80 0                    Info Windows Mobile Broadband Class Driver Event Provider
w 04-01 12:39:12.808 P0004 T0376 mbbcx         EvtCxPreD0Entry: previousPowerState: 3                                                               EvtCxPreD0Entry      mbxdevice_cpp1583 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.808 P0004 T0376 cxwmbclass    EvtDeviceD0Entry: previousPowerState: 3                                                              EvtDeviceD0Entry     power_cpp19 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.808 P0004 T0376 usbbus        Entered Enabled=1                                                                                    MbbBusSetNotificationState businit_c2606 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.808 P0004 T0376 usbbus        MbbUsbDeviceStartDataPipes: Entered                                                                  MbbUsbDeviceStartDataPipes datapipe_c228 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.809 P0004 T0376 usbbus        MbbUsbDeviceStartDataPipes: Exited                                                                   MbbUsbDeviceStartDataPipes datapipe_c286 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.809 P0004 T0376 mbbcx         MbxDevice::PostD0EntryPostHardwareEnabled: previousPowerState: 3                                     MbxDevice::PostD0EntryPostHardwareEnabled mbxdevice_cpp1933 TRACE_LEVEL_INFORMATION
e 04-01 12:39:12.810 P0004 T0376 Microsoft-Windows-NDIS Miniport {c2d9b876-8b20-4cdd-a944-044fd39a97dc}, DeviceState[0x1]                                    Power                0 Microsoft-Windows-NDIS
e 04-01 12:39:12.812 P0004 T0376 Microsoft-Windows-NDIS Miniport {156ce913-cc77-487d-8838-4811ce860b0e}, DeviceState[0x1]                                    Power                0 Microsoft-Windows-NDIS
e 04-01 12:39:12.813 P0004 T0376 Microsoft-Windows-NDIS Miniport {1e58668f-811b-407d-b288-e1f57a432a24}, DeviceState[0x1]                                    Power                0 Microsoft-Windows-NDIS
e 04-01 12:39:12.815 P0004 T0376 Microsoft-Windows-NDIS Miniport {468c0f8c-df7f-4619-85fd-c24ccebdeda3}, DeviceState[0x1]                                    Power                0 Microsoft-Windows-NDIS
w 04-01 12:39:12.815 P0004 T0376 mbbcx         MbxDevice::EnableWakeReasonReporting                                                                 MbxDevice::EnableWakeReasonReporting mbxdevice_cpp2099 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 cxwmbclass    EvtDeviceDisarmWakeFromS0: The device is disarmed for wake                                           EvtDeviceDisarmWakeFromS0 power_cpp130 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 mbbcx         MbxDevice::DisarmWake: Start                                                                         MbxDevice::DisarmWake mbxdevice_cpp1685 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 mbbcx         [ReqMgr][ReqId=0x04ae] Internal Request created [RequestContext=0xFFFFE38624757650]                  MbbReqMgrCreateRequest requestmanager_cpp713 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 mbbcx         [ReqFsm][ReqId=0x04ae] Transition: MbbRequestStateReady -> MbbRequestStateDispatching event=MbbRequestEventDispatch MbbReqMgrQueueEvent  requestmanager_cpp1002 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 mbbcx         [ReqMgr][Timer] MbbTimerTypeRequest already armed at 3fc53, not re-arming                            MbbReqMgrTimerArm    requestmanager_cpp1269 TRACE_LEVEL_WARNING
w 04-01 12:39:12.815 P0004 T0376 mbbcx         [ReqMgr][ReqId=0x04ae], IsPoweredRequest [0x00000000(FALSE)], IsSerialized[0x00000001(TRUE)], IsQueueEmpty[0x00000001(TRUE)], DispatchRequest [0x00000001(TRUE)] MbbReqFsmDispatching requestmanager_cpp1522 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 mbbcx         [ReqFsm][ReqId=0x04ae] Transition: MbbRequestStateDispatching -> MbbRequestStateSendPending event=MbbRequestEventStart MbbReqMgrQueueEvent  requestmanager_cpp1002 TRACE_LEVEL_INFORMATION
e 04-01 12:39:12.815 P0004 T0376 Windows Mobile Broadband Class Driver Event Provider Sending command with the following parameters:
Caller Request Id: 0x0
Driver Request Id: 0
Service Id: {000004ae-cc33-a289-bbbc-4f8bb6b0133e}
Command Name: REDACTED-EMBEDDED-HEXREDACTED-EMBEDDED-HEXREDACTED-EMBEDDED-HEXREDACTED-EMBEDDED-HEXBASIC_NOTIFY_DEVICE_SERVICE_UPDATES
Command Id: 19
Payload Length: 324
Payload: 0x0600000034000000640000009800000028000000C000000018000000D80000001C000000F400000034000000280100001C000000A289CC33BCBB8B4FB6B0133EC2AAE6DF140000000100000002000000030000000400000005000000060000000700000008000000090000000A0000000B0000000C0000000D0000000F000000100000001300000014000000150000001600000017000000533FBEEB14FE44679F9033A223E56C3F050000000100000002000000030000000400000005000000E550A0C85E82479E82F710ABF4C3351F01000000010000001D2B5FF70AA148B2AA5250F15767174E0200000001000000030000003D01DCC5FEF54D050D3ABEF7058E9AAF08000000010000000300000004000000050000000600000007000000080000000A00000068223D049F6C4E0F822D28441FB72340020000000100000002000000 0                    Info Windows Mobile Broadband Class Driver Event Provider
e 04-01 12:39:12.815 P0004 T0376 Windows Mobile Broadband Class Driver Event Provider for OPN Sending command MessageType: 0x3, MessageLength: 372, MessageTransactionId: 533, TotalFragments: 1, CurrentFragment: 0, ServiceId: {a289cc33-bcbb-8b4f-b6b0-133ec2aae6df}, CommandId: 19, CommandType: 1, InformationBufferLength: 324, InformationBuffer: 0x0600000034000000640000009800000028000000C000000018000000D80000001C000000F400000034000000280100001C000000A289CC33BCBB8B4FB6B0133EC2AAE6DF140000000100000002000000030000000400000005000000060000000700000008000000090000000A0000000B0000000C0000000D0000000F000000100000001300000014000000150000001600000017000000533FBEEB14FE44679F9033A223E56C3F050000000100000002000000030000000400000005000000E550A0C85E82479E82F710ABF4C3351F01000000010000001D2B5FF70AA148B2AA5250F15767174E0200000001000000030000003D01DCC5FEF54D050D3ABEF7058E9AAF08000000010000000300000004000000050000000600000007000000080000000A00000068223D049F6C4E0F822D28441FB72340020000000100000002000000 0                    Info Windows Mobile Broadband Class Driver Event Provider for OPN
w 04-01 12:39:12.815 P0004 T0376 usbbus        Sending 372 bytes on control channel                                                                 MbbBusSendMessageFragment businit_c1472 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0004 T0376 usbbus        SetActivityIdForRequest succeeded. Set request activityId = 207b1c4a-085c-0001-270f-83205c08d601     SetActivityIdForRequest businit_c1383 TRACE_LEVEL_INFORMATION
e 04-01 12:39:12.815 P0004 T0376 Windows Mobile Broadband Class Driver Event Provider [1] Send encapsulted command MessageType=0x3, MessageLength=372, TransactionId=533, TotalFrags=1, CurrentFrag=0, ServiceId={33cc89a2-bbbc-4f8b-b6b0-133ec2aae6df}, CID=19, CommandType=1, InfoLength=324 0                    Info Windows Mobile Broadband Class Driver Event Provider
w 04-01 12:39:12.815 P0004 T0376 mbbcx         [Util][ReqId=0x04ae][TID=0x00000215] Pending send Fragment 00/01                                     MbbUtilSendMessageFragments util_cpp1269 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0000 T0000 usbbus        CompletionRoutine() for request 00001C79D4105668 status=STATUS_SUCCESS                               SendCompletionRoutine businit_c1398 TRACE_LEVEL_INFORMATION
w 04-01 12:39:12.815 P0000 T0000 mbbcx         [Util][ReqId=0x04ae][TID=0x00000215] 01/01 fragment completed with status=STATUS_SUCCESS             MbbUtilSendMessageFragmentComplete util_cpp1401 TRACE_LEVEL_INFORMATION
e 04-01 12:39:12.815 P0000 T0000 Windows Mobile Broadband Class Driver Event Provider Sending command completed with status STATUS_SUCCESS. Command was sent with the following parameters:
```