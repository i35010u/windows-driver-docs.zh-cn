---
title: MB 数据连接
description: MB 数据连接
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: dbf9de0980e0ba718c589f1c7e12c2ed2ab5fe89
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250446"
---
# <a name="mb-data-connectivity"></a>MB 数据连接

## <a name="summary"></a>总结

- 数据连接组件如何交互 
  - [Windows 中的移动通信体系结构](#cellular-architecture-in-windows)
  - [基本数据连接所涉及的组件的常规块示意图](#general-block-diagram-of-components-involved-in-basic-data-connectivity)
  - [默认上下文控制器与其直属邻居之间的交互](#interactions-between-the-default-context-controller-and-its-immediate-neighbors)
- [默认上下文控制器](#default-context-controller)如何管理 internet 数据连接
- WWAN 服务与调制解调器之间的[数据连接流动](#mb-data-connectivity-flows)
- [硬件实验室工具包 (HLK) 测试](#hardware-lab-kit-hlk-tests)
- [手动测试](#manual-tests) 手机网络连接
- [MB 数据连接故障排除指南](#mb-data-connectivity-troubleshooting-guide)

## <a name="cellular-architecture-in-windows"></a>Windows 中的移动通信体系结构
OS 中的移动电话堆栈的主要 vssconnection 是 **WWAN 服务 (WwanSvc)** 控制和设置所有数据连接、状态和事件。
它与几个客户端驱动程序交互，以便在操作系统间实现活动。

![WWANSVC 外部交互](images/mb-wwansvc-external-interaction-diag.png "WWANSVC 外部交互")

上图中的首字母缩写：

- **COSA：** Country & 操作员设置资产
- **CSP：** 配置服务提供程序
- **GP 编辑器：** 组策略编辑器
- **MDM：** 移动设备管理
- **MBBCx：**  移动宽带 WDF 类扩展
- **MO：** 移动运营商
- **MV：** 将 Multivariant 与 COSA 数据库中的相应数据相关联的 (framework) 
- **NDISUIO：** NDIS Usermode i/o
- **NQM：** 网络静默模式
- **OEM：** 原始设备制造商
- **OMA：** 开放移动联盟–设备管理
- **OMA-URI：** 打开移动联盟–客户端预配
- **SCM：** 服务控制管理器
- **WCM：** Windows 连接管理器
- **WMI：** Windows Management Instrumentation
- **WNF：** Windows 通知设备
- **WWANPROT DIM：** WWAN 协议驱动程序接口模型
- **wwansvc：** WWAN 服务

有关单个组件的详细信息，请参阅 [移动通信体系结构](cellular-architecture-and-driver-model.md)。

## <a name="general-block-diagram-of-components-involved-in-basic-data-connectivity"></a>基本数据连接所涉及的组件的常规块示意图

主状态机驻留在默认上下文控制器及其关联的上下文生命周期对象中。

![WWANSVC 内部交互](images/mb-wwansvc-internal-interaction-diag.png "WWANSVC 内部交互")

## <a name="interactions-between-the-default-context-controller-and-its-immediate-neighbors"></a>默认上下文控制器与其直属邻居之间的交互
![默认上下文控制器](images/mb-default-context-controller-diag.png "默认上下文控制器")

## <a name="default-context-controller"></a>默认上下文控制器
默认上下文控制器控制 internet 数据连接。
它通过自动连接或手动连接来管理移动电话数据连接基础，无论是使用还是不使用配置文件。

默认上下文控制器执行以下任务：

-  对 internet 连接执行自动连接、重试和自动重试
-  每个主/物理接口都有一个默认上下文控制器实例，其中每个实例：
   - 接收并保留来自各种来源的相关策略设置
   - 接收并保留相关状态信息 (SIM 状态、注册状态、数据包服务状态、iWLAN 状态、ICCID/IMSI 等。 ) 
-  MBB 配置文件评估
   - 评估 MBB 配置文件是否适用于当前策略设置和移动电话状态

-  在 Vibranium 版本或更早版本中：
   - 跟踪相关 MBB 配置文件的添加/删除/更新，并保留这些配置文件的列表
   - 选择要激活的配置文件 (优先级环、上一个配置文件、自动连接订单、LKG 配置文件、购买配置文件、预配的上下文配置文件等 ) 

-  在 Manganese 版本中：
   - 配置文件管理员处理要激活的配置文件选择 
-  回退间隔计算和计时器
-  处理移动电话 Internet 手动连接请求 (配置文件或无配置文件模式) 
-  使用 CWwanContextLifeCycle 类的实例激活与 MBB 配置文件的连接
 
默认上下文控制器使用有限状态机来管理其任务。 

### <a name="finite-state-machine-transitions-of-the-default-context-controller"></a>默认上下文控制器的有限状态机转换
![默认上下文控制器 FSM](images/mb-default-context-controller-fsm-diag.png "默认上下文控制器 FSM")

### <a name="auto-connect"></a>自动连接
#### <a name="policy-settings-that-need-to-be-met-for-auto-connect"></a>自动连接需要满足的策略设置
|策略设置|配置来源|配置单元|
|---|---|---|
|EnabledInternet|通过电话中的用户界面| 每系统|
|highestConnCategory | 通过 UI 的管理员/用户/操作员/设备|  每个接口
|ClientDisableAutoConnect | 通过桌面中的 UI 的用户| 每个接口
|OperatorServiceEnablement| 通过 OTA 从 MO|每个接口
|GPolicyDisableAutoConnect |通过注册表的组策略| 每系统
|mdmDataEnablementPolicy | 从 MDM 通过 WNF (OnEnforced/OffEnforced/NoPolicy) 通知| 每系统
|mdmRoamingPolicy | 从 MDM 通过 WNF (DisabledEnforced/EnabledEnforced/NoPolicy) 通知| 每系统

#### <a name="states-that-need-to-be-concerned-about-auto-connect"></a>需要关注自动连接的状态
|状态|值|
|---|---|
|系统电源状态 | S0/S3/S4/D0/D3/D4
|设备电源状态 | D0/D3/D4
|就绪状态 | 初始化/ICCID 
|IMSI | 影响 IMSI 的配置文件的适用性
|IWLAN 状态 | 仅影响 IWLAN/OK 配置文件的适用性
|注册状态 | 家庭/漫游/合作伙伴
|提供者 ID | 可能会取消备份并触发立即重试
|数据包服务状态 | 分离/附加
|当前数据类 | 可能会行程 highestConnCategory 策略，并影响数据类可配置的配置文件的适用性
|RnR 状态 | 正在进行 RnR

#### <a name="mb-profile-applicability-for-auto-connect"></a>MB 配置文件适用于自动连接
-  SimIccID：必须与接口 (当前 SIM 的 ICCID，但 AnyICCID) 除外
-  IsAdditionalPdpContextProfile：必须为 false (除了购买配置文件) 
-  ConnectionMode：自动或自动主页
-  ProfileCreationType：在 highestConnCategory (Admin/User/Operator/Device) 
-  CellularClass (v4) ： 3GPP/3GPP2 
-  RATApplicability (v4) ： LTE_eHRPD/3GPP_LEGACY
-  RoamApplicability (v4) ： NonPartnerOnly/PartnerOnly/HomeOnly/HomeAndPartner/PartnerAndNonpartner/AllRoaming;iWLAN 配置文件和 iWLAN 除外
-  IMSI (v4) ：如果存在，则必须与当前 IMSI 匹配。 对于多应用 Sim
-  AdminEnable (v4) ：未以管理员身份禁用
-  AdminRoamControl (v4) ：不是管理式漫游-除了 iWLAN 配置文件和 iWLAN 可用以外
####  <a name="selection-of-mbb-profiles-for-auto-connect-in-vb"></a>在 VB 中选择自动连接的 MBB 配置文件
- 优先级环：
    - 基于 [ProfileCreationType](/windows/win32/mbn/schema-profilecreationtype-mbnprofile-element)： AdminProvisioned、UserProvisioned、OperatorProvisioned 和 DeviceProvisioned。
    - 较高优先级环路中适用的配置文件在优先级较低的环中排除了所有配置文件。
- 调制解调器预配配置文件：
    - 基于预配的上下文。
    - 与具有微妙细节的 DeviceProvisioned 配置文件具有相同的环。
- 购买配置文件非常特殊。
- 一轮自动连接和重试次数： 
    - 将尝试所有适用的配置文件中的所有适用的配置文件，以及所有适用的购买配置文件。
    - 一轮中的每个配置文件最多有一个机会。
    - 如果使用有效的 IP 成功连接到配置文件，则会停止循环，并将配置文件指定为最后一个已知良好的 (LKG) 配置文件。
#### <a name="order-of-profiles-in-one-round-of-attempts-in-vb"></a>VB 中一轮尝试中的配置文件顺序
如果一轮尝试包含多个 MBB 配置文件，则顺序为：
- LKG 配置文件（如果存在），并且为非购买配置文件。
- 未购买的调制解调器预配配置文件。 如果有多个，则不指定这些配置文件的顺序。 
- 所有非购买配置文件都具有显式 AutoConnectOrder，按递增 AutoConnectOrder 的顺序排列。 如果 AutoConnectOrder 有多个配置文件，则不会指定这些配置文件的顺序。
- 没有显式 AutoConnectOrder 的所有非购买配置文件。 如果有多个，则不指定这些配置文件的顺序。
- 所有购买配置文件。 如果有多个，则不指定这些配置文件的顺序。 
#### <a name="exponential-back-off"></a>指数回退
-  在出现故障后重试之前，暂停一段时间，以在重试循环中激活所有适用的 MBB 配置文件。
-  用于随机访问媒体的常用方法，避免在发生冲突后重新发生冲突。
-  当一轮尝试中的所有配置文件都无法连接时，将发生后退。
-  在一轮内两个配置文件的重试之间没有任何回退。
-  基本指数回退算法：初始回退3秒（指数系数3），上限为24小时。 例如：3，9，27，81，...。
-  用于慢速节奏重试的特殊网络原因 (初始回退300秒) ：
    -  WWAN_ERR_3GPP_SO_NOT_SUBSCRIBED，//33
    -  WWAN_ERR_3GPP_AUTH_FAILURE、//29
    -   WWAN_ERR_3GPP_INSUFFICIENT_RESOURCES，//26
    -   WWAN_ERR_3GPP_UNKNOWN_PDP_ADDRESS_TYPE，//28
    -   WWAN_ERR_3GPP_ACTIVATION_REJECT/
-  OEM 可以自定义初始的备份。 每个代码可以具有以下三个类别之一：
    -  正常-步调：与基本事例相同 (3 秒) 
    -  缓慢进度：300秒
    -  Glacier：24小时 (几乎不重试) 

#### <a name="back-off-cancelation-or-back-off-timer-expiration"></a>后关闭或回退计时器过期
- 在以下情况下，可以取消备份并立即重试开始：
    - 来自 WCM 的自动连接提示
    - 添加或更新自动连接 MBB 配置文件
    - 设备漫游到其他 MO
    - 最高连接类别策略已更改
    
- 如果在备份期间发生手动连接请求，则会取消备份，并手动连接过程开始。

- 将取消备份，并且在以下情况下不会发生自动连接：
    - SIM 会被删除。
    - 手机网络状态不再可用于连接 (例如，在注销或分离) 期间。
    - 已吊销自动连接令牌。
    - 手机网络数据已禁用。
    - 其他策略设置已更改，因此不可能再进行自动连接。
    - 以后的事件可能会重新触发自动连接，因为该操作已取消，并且不进行自动连接。

- 当回退计时器自然过期时，重试开始，并执行与初始自动连接相同的操作。

### <a name="manual-connect"></a>手动连接
- 通过 wwansvc RPC API 从外部启动数据连接的引入：
    - 在移动电话设置 UI 或网络浮出控件中，用户取消选中 "让 Windows 保持此连接" 框，然后单击 "连接" 按钮。
    - 从 Windows 8 开始，WCM 还可能会引入数据连接。
    - 仅当未在 (空闲或备份关闭) 进行自动连接时，才允许手动连接。
    
- 可以使用或不使用特定 MBB 配置文件发出连接请求。 由于 RS2 的原因：
    - 如果给定了特定 MBB 配置文件，则仅使用该 MBB 配置文件进行连接。
    - 如果未提供特定的 MBB 配置文件，则默认上下文控制器将选取 MBB 配置文件，并逐个尝试该配置文件，直到连接成功激活并使用 MBB 配置文件或它们无法连接。
    
- 受限于与自动连接相同的一组策略设置。
    
- 受限于自动连接的一组类似的移动电话状态信息和限制。
    
- MBB 配置文件适用性服从一组类似的规则，例如自动连接，但有一个值得注意的例外情况：
    - ConnectionMode 为 "手动" 的 MBB 配置文件适用于 "手动连接"。 
    
- MBB 配置文件选择和顺序与自动连接相同。
    
- 如果未提供特定的 MBB 配置文件，并且 a 轮中的 MBB 配置文件无法成功连接，则手动连接请求已完成，但失败。 没有备份，不重试。
    
- 如果给定了特定 MBB 配置文件，并且 MBB 配置文件无法成功连接，则手动连接请求已完成，但失败。 没有备份，不重试。
    
- 如果成功连接的手动连接在稍后 unsolicitedly 断开连接，则会报告状态，但不会进行任何备份，也不会重试。

## <a name="mb-data-connectivity-flows"></a>MB 数据连接流

[OID_WWAN_CONNECT](oid-wwan-connect.md) 用于启动与调制解调器的连接。 下面是描述与调制解调器的数据连接的流。

### <a name="successful-activation"></a>成功激活

![成功的 PDP 上下文激活](images/mb_successful_activation.png "成功的 PDP 上下文激活流")

### <a name="successful-deactivation"></a>成功停用

![成功的 PDP 上下文停用](images/mb_successful_deactivation.png "成功的 PDP 上下文停用流")


### <a name="manual-connect"></a>手动连接

![手动连接](images/mb_manual_connect.png "手动连接流")

## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试

将测试计算机与 ATT SIM 连接到 HLK 服务器。

请参阅 [安装 HLK 的步骤](https://microsoft.sharepoint.com/teams/HWKits/SitePages/HWLabKit/Manual%20Controller%20Installation.aspx)。 

在 HLK Studio 中，连接到设备移动电话调制解调器驱动程序并运行测试： [Win6_4。GSM.TestConnect](/windows-hardware/test/hlk/testref/b5a998f3-bd1c-47aa-bcf3-6c9092935e1c)。

或者，运行 **TestConnect** HLK testlist by [**netsh**](/windows-server/networking/technologies/netsh/netsh-mbn) 和 [**netsh-mbn**](mb-netsh-mbn-test.md)。

```
netsh mbn test feature=connectivity param="AccessString=internet"
```
显示 HLK 测试结果的文件应已在运行 "netsh mbn test" 命令的目录中生成。

## <a name="manual-tests"></a>手动测试
### <a name="after-reboot-cellular-auto-connects"></a>重新启动后，手机网络自动连接
1. 在 Wi-Fi 切换后，验证活动的手机网络连接。 托盘应显示手机网络连接栏，并且 internet 浏览应正常工作。
1. 重新启动 DUT。 重新启动后，验证是否存在活动的手机网络连接。 托盘应显示手机网络连接栏。 

### <a name="browse-internet-using-cellular-data-with-new-sim"></a>使用新 SIM 的手机网络数据浏览 Internet
1. 插入包含活动数据计划的 SIM 卡。 如果设备已有 SIM 卡，请弹出 SIM 卡，并插入其他操作员提供的不同 SIM 卡。
1. 在 Wi-Fi 切换后，验证活动的手机网络连接。 从屏幕顶部向下轻扫可打开快速操作中心，而托盘应显示手机网络连接栏和数据图标。

### <a name="connect-cellular-manually"></a>手动连接手机网络
1. 将以太网拔出并 Wi-Fi 关闭后，请在手机网络设置中取消选中 "允许 Windows 管理此连接"。
1. 重新启动 DUT。
1. 启动后，打开手机网络设置并单击 "连接到手机网络"。 移动电话应连接，internet 浏览应正常工作。

### <a name="after-wake-from-hibernation-s4-cellular-auto-connects"></a>从休眠状态唤醒 (S4) 后，手机网络自动连接
  1. 确保在 "移动电话" 设置中选中 "允许 Windows 管理此连接"。
  1. 将 DUT 放入 S4。
  1. 唤醒 DUT 并验证它是否会自动建立手机网络连接。 用户应能够浏览 internet。
### <a name="after-wake-from-hibernation-s4-connect-cellular-manually"></a>从休眠唤醒 (S4) 后，手动连接手机网络
  1. 将以太网拔出并 Wi-Fi 关闭后，请在手机网络设置中取消选中 "允许 Windows 管理此连接"。
  1. 在管理员命令提示符下运行命令： shutdown-h 
  1. 计算机将处于休眠状态。 超过30秒后，按下计算机的电源按钮，从休眠状态唤醒。 重新登录，打开 "手机网络设置"，然后单击 "连接到手机网络"。  移动电话应连接，用户应能浏览 internet。
### <a name="after-wake-from-screen-sleep-cellular-auto-connects"></a>从屏幕睡眠状态唤醒后，手机网络自动连接
  1. 将以太网拔出并 Wi-Fi 关闭后，验证活动的手机网络连接。
  1.  (可选) 使屏幕进入睡眠状态。 可以在 "设置" 下将屏幕睡眠设置为1分钟，> 系统 > Power & 睡眠。 此设置不应设置为 "从不"。
  1. 使用鼠标或键盘唤醒屏幕，并重新登录。 手机网络应保持连接状态，并且用户应该能够通过 VAIL/WCOS) 的容器浏览 internet (。

## <a name="mb-data-connectivity-troubleshooting-guide"></a>MB 数据连接故障排除指南
1. 可以使用以下说明收集和解码日志： [MB 收集日志](mb-collecting-logs.md)
1. 打开[TextAnalysisTool](mb-analyzing-logs.md)中的 .txt 文件。
1. 加载 [Bacis 连接筛选器](mb-basic-connectivity-tat.md)

### <a name="sample-log-for-disconnect-success"></a>断开连接成功的示例日志：
```
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanManager::EnumerateInterfaces Message:  Number of interfaces returned: 1"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanDataExecutor::WwanDisconnect InterfaceGuid:    {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     connectionID 0x0"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanDefaultContextController::WwanDisconnect Message:  Disconnect (connectionId:85) Invoked"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanDefaultContextController::fsmEventHandler InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""entry with state: 4, event: 15 (EXEC 0)"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanDefaultContextController::fsmEventHandler_Connected Message:   manual disconnecting" 
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  WwanNhTraceMsmNotification InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""[NH] Dispatch WwanNotificationSourceMsm\WwanMsmEventTypeConnectionIStreamUpdated ConnectionIStream[Intf={F1A7855C-27F0-433D-9BCD-55E1068C4F41} Prfl[Name= Guid= Conn=] State[Ready=1 Register=3 Activation=4] contextState NwError = 0x0, apiInfoResult = 0x0]"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::fsmEventHandler Message:     entry with state 4 Event 1"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::CleanUpFull Message:     Starting to Cleanup the Context LifeCyle"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::SetProfileIndex InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""set profile index, profile index 20000006"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "   InterfaceGuid={f1a7855c-27f0-433d-9bcd-55e1068c4f41},RequestId=0x8C,,cbPayload=131614,Payload=0x1C000000060000200118C01E340300000A000000C8000000983A0000,ErrorCode=The operation completed successfully."
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  WwanTxSendReq Message:  OID (Code: 23 Type: 0) sent and completed"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  wwanTxmAoAcRefHandler InterfaceGuid:    {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     Acquiring AoAc Ref for Parent Interface before sending a TX [0x8d]"
TraceLog    Microsoft-Windows-wmbclass  24:09.5 "Instance:  1 request:  0xFFFFCD067126BF00 OID:     0xE01010C OID name:     OID_WWAN_CONNECT RequestId:     0x8D RequestHandle:     0x0 Type:   1 InformationLength:    1260"
TraceLog    Microsoft-Windows-wmbclass  24:09.5 "Instance:  1 Request:  0xFFFFCD067126BF00 Status:  The operation that was requested is pending completion." TraceLog   Microsoft-Windows-wmbclass  24:09.5 "CallerRequestId:   0x8D DriverRequestId:   0 ServiceId:    {00000274-cc33-a289-bbbc-4f8bb6b0133e} CommandName:     ???¦????BASIC_CONNECT CommandId:    12 InBufferSize:    116 Payload:    0x00000000000000003C0000001A000000580000000A00000064000000100000000000000000000000000000007E5E2A7E4E6F7272736B656E7E5E2A7E6D006900630072006F0073006F00660074002E0063006F006D000000610064006D0069006E000000700061007300730077006F0072006400" 
TraceLog    Microsoft-Windows-wmbclass  24:09.5 "Instance:  1MessageType:   0x3 MessageLength:  164 MessageTransactionId:   54TotalFragments:   1CurrentFragment:   0 ServiceId:    {33cc89a2-bbbc-4f8b-b6b0-133ec2aae6df} CID:     12 CommandType:     1 InfoLength:   116"
TraceLog    Microsoft-Windows-wmbclass  24:09.5 "CallerRequestId:   0x8D DriverRequestId:   0 ServiceId:    {00000274-cc33-a289-bbbc-4f8bb6b0133e} CommandName:     ???¦????BASIC_CONNECT CommandId:    12 InBufferSize:    116 Payload:    0x00000000000000003C0000001A000000580000000A00000064000000100000000000000000000000000000007E5E2A7E4E6F7272736B656E7E5E2A7E6D006900630072006F0073006F00660074002E0063006F006D000000610064006D0069006E000000700061007300730077006F0072006400 NdisStatus:  STATUS_SUCCESS"
TraceLog    Microsoft-Windows-wmbclass  24:09.5 "Instance:  1 Request:  0xFFFFCD067126BF00 OID:     0xE01010C OID name:     OID_WWAN_CONNECT RequestId:     0x8D RequestHandle:     0x0 Type:   1 BytesUsed:    1260 BytesNeeded:   0 Status:   The request will be completed later by NDIS status indication."
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  WwanTxSendReq Message:  OID (Code: 12 Type: 0 timeoutInSec: 199) sent to dim and pending solicited notif"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  WwanTimerWrapper::StartTimer Message:   Timer (ID = 0) Start Completed"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  WwanTxmEvaluateArmTimer InterfaceGuid:  {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""TXM timer armed for 199 seconds expire 0x4e42f9, TxmHandle=(0x2)"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  _sendReq Message:   ASYNC OID (pTx->handle: 000000000000008D Code: 12) sent (time 0x4b39a1)"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::SendMbbConnectReq InterfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     OID_WWAN_CONNECT (Deactivate): ReqHandle 0x8d ReqID 0x60 ConnID 0x55 APN [microsoft.com] IPType (sent 0 confg 0) Auth 0 PwdP 1 MediaPref 1 PrefSrc 4"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::StartTimer Message:  Timer Start Completed"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::CleanUpFull Message:     Completed Cleanup of the Context LifeCyle" 
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanContextLifeCycle::fsmEventHandler Message:     exit with state 6"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanDefaultContextController::fsmEventHandler InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     exit with state 5 (EXEC 0)" 
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanResetRecovery::fsmEventHandler InterfaceGuid:  {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     "" entry with state: 3, event: 0"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanResetRecovery::fsmEventHandler InterfaceGuid:  {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     "" exit with state: 1, event: 0, RnR stage: 0 Potent RnR: 0"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "InterfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41}"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  WwanNhTraceMsmNotification InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     [NH] Dispatch WwanNotificationSourceMsm\WwanMsmEventTypeIStreamChanged (RegistrationState: 3)"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "FunctionCall:  CWwanDataExecutor::GetConnectionInfo InterfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     isPhysi 1 PS 2 isIWLANAvail 0 isConnected 0"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "interfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41}"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "mbnInterface:  {F1A7855C-27F0-433D-9BCD-55E1068C4F41} info:    12301"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 "mbnInterface:  {F1A7855C-27F0-433D-9BCD-55E1068C4F41} info:    MS MBN"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   24:09.5 " Message:  WWAN_INTERFACE_OBJECT::readyObject.readyInfo.ReadyState=1"
```

### <a name="sample-log-for-connect-success"></a>连接成功的示例日志：
```
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanManager::EnumerateInterfaces Message:  Number of interfaces returned: 1"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataExecutor::WwanConnect Message:     ""Connect (connMode:0, str:!!##MBIMModemProvisionedContextV2InternetProfile##098765432109876) Invoked"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataExecutor::WwanConnect Message:     ""Connect (flags 0x0, apiStartTime 4996546 isUserStarted 1 isLowBoxMBAERequest 0"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "InterfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41} ModemIndex:  0 ExecutorIndex:    0 ProfileName:  !!##MBIMModemProvisionedContextV2InternetProfile##098765432109876 ProfileSource:    WwanProfileModemProvisioned connMode:   WwanConnectionModeProfile"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDefaultContextController::IsAllowedByRoamingPolicies Message:  return TRUE"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWWANContextControllerBase::FillProfileGuidInCIS Message:   [ConnectionIStream] Updated PrflGuid={64CFE041-9925-4109-B738-9C9F7EC95A92}"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDefaultContextController::WwanConnect Message:     manual connection request: temp conn ID 0x61 APN [microsoft.com]"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDefaultContextController::fsmEventHandler InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""entry with state: 0, event: 14 (EXEC 0)"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDefaultContextController::IsAllowedByRoamingPolicies Message:  return TRUE"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataExecutor::DisconnectMatchingAdditionalPdpContexts Message:     ""Looking for APN: microsoft.com, IPType: 0"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataResourceManager::CheckResourceMaxContextCountByOEM Message:    non-CDMA"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataResourceManager::CheckResourceMaxContextCountByOEM Message:    ""per IMSI OEM configred MaxNumberOfPDPContexts not found, trying device settings."""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataResourceManager::CheckResourceMaxContextCountByOEM Message:    ""device OEM configred MaxNumberOfPDPContexts not found, using default settings."""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataResourceManager::SetPdpContextsOEMConfigured Message:  OEMConfig using 8"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataResourceManager::UpdatePdpContexts Message:    ""OEMConfiged 8, Modem supports 17, using 8"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataResourceManager::ExecutorAcquireResourceMessage:   Acquired Resource Count 1"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  WwanNhTraceMsmNotification InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""[NH] Dispatch WwanNotificationSourceMsm\WwanMsmEventTypeConnectionIStreamUpdated ConnectionIStream[Intf={F1A7855C-27F0-433D-9BCD-55E1068C4F41} Prfl[Name=!!##MBIMModemProvisionedContextV2InternetProfile##098765432109876 Guid={64CFE041-9925-4109-B738-9C9F7EC95A92} Conn=] State[Ready=1 Register=3 Activation=2] contextState NwError = 0x0, apiInfoResult = 0x0]"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDefaultContextController::StartContextLifeCycleWrapper Message:    Manual connecting on profile !!##MBIMModemProvisionedContextV2InternetProfile##098765432109876 ConnID 97"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanContextLifeCycle::fsmEventHandler Message:     entry with state 0 Event 0"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanContextLifeCycle::SetProfileIndex InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""set profile index, profile index 20000006"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "   InterfaceGuid={f1a7855c-27f0-433d-9bcd-55e1068c4f41},RequestId=0x8E,,cbPayload=131614,Payload=0x1C000000060000200118C01E340300000A000000C8000000983A0000,ErrorCode=The operation completed successfully."
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  WwanTxSendReq Message:  OID (Code: 23 Type: 0) sent and completed"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  wwanTxmAoAcRefHandler InterfaceGuid:    {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     Acquiring AoAc Ref for Parent Interface before sending a TX [0x8f]"
TraceLog    Microsoft-Windows-wmbclass  25:16.1 "Instance:  1 Request:  0xFFFFCD06728F7160 OID:     0xE01010C OID name:     OID_WWAN_CONNECT RequestId:     0x8F RequestHandle:     0x0 Type:   1 InformationLength:    1260"
TraceLog    Microsoft-Windows-wmbclass  25:16.1 "Instance:  1 Request:  0xFFFFCD06728F7160 Status:  The operation that was requested is pending completion."
TraceLog    Microsoft-Windows-wmbclass  25:16.1 "CallerRequestId:   0x8F DriverRequestId:   0 ServiceId:    {00000281-cc33-a289-bbbc-4f8bb6b0133e} CommandName:     Ã‚ÂªÃ¦ÃŸBASIC_CONNECT CommandId:    12 InBufferSize:    116 Payload:    0x00000000010000003C0000001A000000580000000A00000064000000100000000000000000000000000000007E5E2A7E4E6F7272736B656E7E5E2A7E6D006900630072006F0073006F00660074002E0063006F006D000000610064006D0069006E000000700061007300730077006F0072006400"
TraceLog    Microsoft-Windows-wmbclass  25:16.1 "Instance:  1 MessageType:  0x3 MessageLength:  164 MessageTransactionId:   55 TotalFragments:  1 CurrentFragment:  0 ServiceId:    {33cc89a2-bbbc-4f8b-b6b0-133ec2aae6df} CID:     12 CommandType:     1 InfoLength:   116"
TraceLog    Microsoft-Windows-wmbclass  25:16.1 "CallerRequestId:   0x8F DriverRequestId:   0 ServiceId:    {00000281-cc33-a289-bbbc-4f8bb6b0133e} CommandName:     Ã‚ÂªÃ¦ÃŸBASIC_CONNECT CommandId:    12InBufferSize:     116Payload:     0x00000000010000003C0000001A000000580000000A00000064000000100000000000000000000000000000007E5E2A7E4E6F7272736B656E7E5E2A7E6D006900630072006F0073006F00660074002E0063006F006D000000610064006D0069006E000000700061007300730077006F0072006400 NdisStatus:  STATUS_SUCCESS"
TraceLog    Microsoft-Win dows-wmbclass 25:16.1 "Instance:  1 Request:  0xFFFFCD06728F7160 OID:     0xE01010C OID name:     OID_WWAN_CONNECT RequestId:     0x8FRequestHandle:  0x0Type:    1BytesUsed:     1260 BytesNeeded:   0 Status:   The request will be completed later by NDIS status indication."
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  WwanTxSendReq Message:  OID (Code: 12 Type: 0 timeoutInSec: 181) sent to dim and pending solicited notif"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  WwanTimerWrapper::StartTimer Message:   Timer (ID = 0) Start Completed"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  WwanTxmEvaluateArmTimer InterfaceGuid:  {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     ""TXM timer armed for 181 seconds expire 0x4f00ca, TxmHandle=(0x2)"""
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  _sendReq Message:   ASYNC OID (pTx->handle: 000000000000008F Code: 12) sent (time 0x4c3dc2)"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanContextLifeCycle::SendMbbConnectReq InterfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     OID_WWAN_CONNECT (Activate): ReqHandle 0x8f ReqID 0x62 ConnID 0x61 APN [microsoft.com] IPType (sent 0 confg 0) Auth 0 PwdP 1 MediaPref 1 PrefSrc 4"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanContextLifeCycle::StartTimer Message:  Timer Start Completed"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanContextLifeCycle::fsmEventHandler Message:     exit with state 2"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDefaultContextController::fsmEventHandler InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41} Message:     exit with state 3 (EXEC 0)
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "InterfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41}"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  WwanNhTraceMsmNotification InterfaceGuid:   {f1a7855c-27f0-433d-9bcd-55e1068c4f41}Message:  [NH] Dispatch WwanNotificationSourceMsm\WwanMsmEventTypeIStreamChanged (RegistrationState: 3)"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  CWwanDataExecutor::GetConnectionInfoInterfaceGuid:  {f1a7855c-27f0-433d-9bcd-55e1068c4f41}Message:  isPhysi 1 PS 2 isIWLANAvail 0 isConnected 0"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "interfaceGuid:     {f1a7855c-27f0-433d-9bcd-55e1068c4f41}"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "mbnInterface:  {F1A7855C-27F0-433D-9BCD-55E1068C4F41}info:     12301"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "mbnInterface:  {F1A7855C-27F0-433D-9BCD-55E1068C4F41}info:     MS MBN"
TraceLog    Microsoft-Windows-WWAN-SVC-EVENTS   25:16.1 "FunctionCall:  _PublishSebNotificationMessage:     WWAN_INTERFACE_OBJECT::readyObject.readyInfo.ReadyState=1"
```
