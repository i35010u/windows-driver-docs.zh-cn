---
title: MB 驱动程序堆栈、挂起和恢复
description: 了解 MBIM 4.0 驱动程序堆栈、挂起和恢复，以及如何对其进行测试和调试。
keywords: Resume、挂、MBIM 4.0、DriverStack
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 94cf1d74f7a3960a687421b78c9bd49bd8d534c1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250536"
---
# <a name="mb-driver-stack-suspend-and-resume"></a>MB 驱动程序堆栈、挂起和恢复 
## <a name="overview"></a>概述

Microsoft 为移动宽带 (MBB) 设备提供了一个用于移动宽带的驱动程序类驱动程序， (MBCD) 。 此驱动程序基于移动宽带接口模型 (MBIM) 规范，它是一种用于 MBB 设备的接口 (也称为调制解调器) 与 Windows 进行通信。 MBIM 规范基于 USB。 MBCD 支持通过一种称为 USB 设备仿真 (UDE) 的技术来模拟 USB 调制解调器和调制解调器。 

MBCD 是一个微型端口驱动程序，它结合了网络驱动程序接口规范 (NDIS) 端口驱动程序构成单个函数驱动程序。 在 OSI 网络模型中，此驱动程序在逻辑上位于数据链接层的上半部分， (第2层) 。 网络协议驱动程序 (如) 逻辑上驻留在网络层上的 IP (第3层) 接收来自传输层 (第4层) 的数据 ()  (UDP) 的网段 (UDP) ，并通过调用 NDIS Api 将数据 (Pdu 发送到数据链路层。 通常，在必要时，NDIS 仅涉及微型端口驱动程序。

<br>
<table style="border:3px #cccccc solid;" cellpadding="10" border='1'>
  <tr>
      <td align ="center" colspan="5">OSI 网络模型</td>
  </tr>
  <tr>
    <td align ="center" colspan="3">层</td>
    <td>协议数据单元 (PDU) </td>
    <td>函数</td>
  </tr>
  <tr>
      <td valign = "center" rowspan="4"> 主机 <br> 层 </td>
        <td> 7</td> 
        <td> 应用程序 </td> 
        <td valign = "center" rowspan = "3"> 数据 </td>
        <td> 高级 Api，包括资源共享和远程文件访问</td>
  </tr>
  <tr>
        <td>6 </td>
        <td> 呈现 </td> 
        <td> 网络服务和应用程序之间的数据转换，包括字符编码、数据压缩和加密 </td>
  </tr>
  <tr>
        <td>5 </td>
        <td> 会话 </td> 
        <td> 管理通信会话，例如两个节点之间的多个来回传输形式的连续信息交换 </td>
  </tr>
    <tr>
        <td>4 </td>
        <td> 运输 </td> 
        <td> 段 </td>
        <td> 可靠地在网络上的点之间传输数据段，包括分段、确认和多路复用 </td>
  </tr>
  <tr>
        <td valign = "center" rowspan="3"> 媒体 <br> 层 </td>
        <td> 3</td> 
        <td> 网络 </td> 
        <td> 数据包 </td>
        <td> 管理和构造多节点网络，包括地址映射、路由和流量控制</td>
  </tr>
  <tr>
        <td> 2 </td>
        <td> 数据链接 </td>
        <td> Frame </td>       
        <td> 可靠地在物理层连接的两个节点之间传输数据帧</td>
  </tr>
  <tr>
        <td> 1 </td>
        <td> 物理 </td>
        <td> 符号 </td>
        <td> 物理介质上的原始位流的传输和接收</td>
  </tr>
</table>
<br>


网络层是网络协议驱动程序所在的位置，包括 NDIS Usermode i/o (NDISUIO) 协议驱动程序。 此驱动程序在控制和配置 MBB 设备方面起到重要作用。 请注意，在概念上，TCP/IP 的 IP 部分驻留在概念上。 你可以将它们视为同级。

WwanSvc 是主要负责对调制解调器的控制、枚举其功能及其配置的服务。 WwanSvc 使用 WWAN Oid 向 NDISUIO 发出命令，这会将这些 Oid 传递到 NDIS。 MBCD 微型端口驱动程序定义它支持的 Oid，并在函数驱动程序的初始化过程中将其提供给 NDIS。 因此，当 NDIS 接收来自 NDISUIO 的 OID 时，它会根据需要使用微型端口。

应用程序中的命令流 (例如移动电话 UI) 如下所示：

应用程序 > WwanSvc--- (OID) --->---- () OID--->---- () ---OID >--- (MBCD) ---> MBB 设备。

以上概述了控制路径所涉及的技术。 数据路径更复杂，因为有多个解决方案已准备就绪。 但是，我们可以将数据路径通用化为：

应用程序 > TCP/IP-- (数据包) --> NDIS---- () ---> [Driver]---> MBB 设备。

[Driver] 可能是旧驱动程序、新式驱动程序或第三方 IHV 驱动程序。

## <a name="driver-architecture"></a>驱动程序体系结构
### <a name="legacy"></a>旧的
![旧的](images/mbim_architecture_legacy.png?raw=true "旧的")

### <a name="current-since-rs5-osbuild-17763"></a>由于 RS5 OSBuild 17763) 的当前 (
![当前](images/mbim_4_0_architecture.png?raw=true "当前")

## <a name="device-power-up"></a>设备开启
![设备通电](images/mbim_powerup.png?raw=true "设备通电")

## <a name="device-power-down"></a>设备断电
![设备断电](images/mbim_powerdown.png?raw=true "设备断电")

## <a name="mbbcx-interface"></a>MBBCx 接口
![MBBCx 接口](images/mbim_interface.png?raw=true "MBBCx 接口")

**另请参阅**

[EvtMbbDeviceSendMBIMFragment](/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_send_mbim_fragment)

[MbbRequestComplete](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbrequestcomplete)

### <a name="default-netadapter-initialization"></a>默认 Get-netadapter 初始化
![默认 Get-netadapter 初始化](images/Default_netadapter_init.png?raw=true "默认 Get-netadapter Init")

**另请参阅**

[MbbAdapterInitialize](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbadapterinitialize)

### <a name="additional-netadapter-initialization"></a>其他 Get-netadapter 初始化
![其他 Get-netadapter Init](images/netadapter_init.png?raw=true "其他 Get-netadapter Init")

### <a name="device-initialization"></a>设备初始化
![设备初始化](images/device_init.png?raw=true "设备初始化")


## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试
请参阅 [安装 HLK 的步骤](https://microsoft.sharepoint.com/teams/HWKits/SitePages/HWLabKit/Manual%20Controller%20Installation.aspx)。

在 HLK Studio 中，连接到设备移动电话调制解调器驱动程序并运行测试： [TestPowerStates](https://docs.microsoft.com/windows-hardware/test/hlk/testref/f0af8e06-4d04-4027-8b84-777a6de4ce49)。

可以通过 netsh 运行 **TestPowerStates** HLK testlist。 有关使用 netsh 工具的详细信息，请参阅 [**mbn**](https://docs.microsoft.com/windows-server/networking/technologies/netsh/netsh-mbn) and [**netsh-mbn**](mb-netsh-mbn-test.md)。

```
netsh mbn test feature=power testpath="C:\\data\\test\\bin" taefpath="C:\\data\\test\\bin"
```

显示 HLK 测试结果的此文件应已在运行 "netsh mbn test" 命令的目录中生成： `TestPowerStates.htm` 。

## <a name="manual-tests"></a>手动测试
### <a name="auto-connect-after-wake-from-hibernation-s4"></a>从休眠唤醒 (S4 后自动连接) 

  1. 确保在 "移动电话" 设置中选中 "允许 Windows 管理此连接"。
  1. 将 DUT 放入 S4。
  1. 唤醒 DUT。 验证它是否会自动建立手机网络连接，并且用户能够浏览 internet。

### <a name="connect-cellular-manually-after-wake-from-hibernation-s4"></a>从休眠唤醒 (S4 后，手动连接手机网络) 

  1. 将以太网拔出并 Wi-Fi 关闭后，请在手机网络设置中取消选中 "允许 Windows 管理此连接"。
  1. 在管理员命令提示符下，运行以下命令： shutdown-h 
  1. 计算机将处于休眠状态。 超过30秒后，按下计算机的电源按钮，从休眠状态唤醒。 重新登录，打开 "手机网络设置"，然后单击 "连接到手机网络"。 移动电话应连接，用户应能浏览 internet。

### <a name="auto-connect-after-wake-from-screen-sleep"></a>从屏幕睡眠中唤醒后自动连接

  1. 将以太网拔出并 Wi-Fi 关闭后，验证活动的手机网络连接。
  1.  (可选步骤) 允许屏幕进入睡眠状态。 可以在 "设置" 下将屏幕睡眠设置为1分钟-> 系统 > Power & 睡眠。 此设置不应设置为 "从不"。
  1. 使用鼠标或键盘唤醒屏幕，并重新登录。 手机网络应保持连接状态，并且用户应该能够浏览 internet，包括 VAIL/WCOS 系统下的。

## <a name="log-analysis"></a>日志分析
### <a name="tips"></a>提示
- 确保日志中包括必要的 ETW 提供程序，包括 MbbCx、NetAdapterCx、WwanSvc 和 NdisUio。
- 检查设备电源状态 (Dx 状态) 和设备电源功能
- 在上面的 power flow 中检查日志
- OID 和指示对
### <a name="sample-log"></a>示例日志
```
597454 [2]1020.115C::2018-08-31 01:05:12.669792000 [WwanService]INFO: CWwanDataExecutor::OnNdisNotification - current device power state 3 (WaitForDeviceD0AfterSleep 1 systemPowerState 0)
679337 [6]1020.115C::2018-08-31 01:07:36.343312200 [WwanService]INFO: CWwanManager::OnSystemPowerStateChange - system resuming from sleep (fWaitForDeviceD0AfterSleep 1)
2422155 [7]1020.1150::2018-08-31 01:07:37.878446100 [WwanService]INFO: CWwanDataExecutor::OnNdisNotification - current device power state 0 (WaitForDeviceD0AfterSleep 1 systemPowerState 1)
2437098 [3]1020.115C::2018-08-31 01:07:37.893061200 [WwanService]INFO: CWwanDeviceEnumerator::onDeviceRemoval: MBB device removed [9d33b700-d66d-4c0a-807f-6a328690dafa].
2678588 [5]1020.2E30::2018-08-31 01:07:40.765642800 [WwanService]INFO: CWwanDeviceEnumerator::onDeviceArrival: MBB device arrived [9d33b700-d66d-4c0a-807f-6a328690dafa]. Parent Interface = [00000000-0000-0000-0000-000000000000].
2679204 [6]1020.2E30::2018-08-31 01:07:40.766278700 [sys]Ref WwanprotGetD3ColdCapability:0x6a2 \DEVICE\{9D33B700-D66D-4C0A-807F-6A328690DAFA} 0x2
2679205 [6]1020.2E30::2018-08-31 01:07:40.766280200 [sys]Sending IRP_MN_QUERY_INTERFACE for interface GUID_D3COLD_SUPPORT_INTERFACE
2679211 [6]1020.2E30::2018-08-31 01:07:40.766287400 [sys]IRP_MN_QUERY_INTERFACE for interface GUID_D3COLD_SUPPORT_INTERFACE succeeded
2679212 [6]1020.2E30::2018-08-31 01:07:40.766289500 [sys]Successfully queried the D3 cold capability of device. D3ColdCapability = 0
2679213 [6]1020.2E30::2018-08-31 01:07:40.766290000 [sys]DeRef WwanprotGetD3ColdCapability:0x6a8 \DEVICE\{9D33B700-D66D-4C0A-807F-6A328690DAFA} 0x2
2679214 [6]1020.2E30::2018-08-31 01:07:40.766290500 [sys]Returning D3 cold capability as 0. Status = c0000225
2679219 [6]1020.2E30::2018-08-31 01:07:40.766294100 [WwanService]CWwanNetworkInterface::InitializeInterface: Getting D3 cold capability for interface 9d33b700-d66d-4c0a-807f-6a328690dafa failed [1168]
2679220 [6]1020.2E30::2018-08-31 01:07:40.766294600 [WwanService]CWwanNetworkInterface::InitializeInterface: fIsEmbedded:0x00000001(true) fIsD3ColdSupported:0x00000000(false)
```


## <a name="see-also"></a>另请参阅
[UDE 体系结构](/windows-hardware/drivers/usbcon/developing-windows-drivers-for-emulated-usb-host-controllers-and-devices)

[NDIS 6.20 简介](/windows-hardware/drivers/network/introduction-to-ndis-6-20)

[MBIM 概述](/windows-hardware/drivers/network/mb-interface-model)

[MBIM 合规性测试修订版本1。0](https://www.usb.org/sites/default/files/MBIM-Compliance-1.0.pdf)

[USB 设备的移动宽带实施指南](/windows-hardware/drivers/network/mobile-broadband-implementation-guidelines-for-usb-devices)

[NetAdapterCx](/windows-hardware/drivers/netcx/)




