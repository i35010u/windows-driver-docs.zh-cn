---
title: Microsoft 定义的蓝牙 HCI 命令和事件
description: 蓝牙主机控制器接口 (HCI) 指定的主机和蓝牙单选控制器之间的所有交互。
ms.assetid: 68E34B92-155B-401E-8D90-5BD1AF036B4D
ms.date: 02/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 400fdb42155f468a03c2570cfa295f269334f44c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903175"
---
# <a name="microsoft-defined-bluetooth-hci-extensions"></a>Microsoft 定义的蓝牙 HCI 扩展

蓝牙主机控制器接口 (HCI) 指定的主机和蓝牙单选控制器之间的所有交互。 蓝牙规范允许使用供应商定义的 HCI 命令和事件，若要启用非标准化的主机和控制器之间的交互。 Microsoft 定义了特定于供应商 HCI 命令和事件是由 Windows。 蓝牙控制器实施者可以使用这些扩展来实现特殊功能。

## <a name="requirements"></a>要求

支持在 Windows 10 桌面版 （主页、 专业版、 企业版和教育版），Windows 10 移动版及更高版本。

## <a name="microsoft-defined-hci-commands"></a>Microsoft 定义的 HCI 命令

蓝牙 HCI 命令由一个 16 位的命令代码标识。 蓝牙组织定义的范围为 0x0000 到 0xFBFF 中的值。 供应商定义在范围内 0xFC00 到 0xFFFF，1024年不同可能供应商指派的命令代码允许的值。

供应商必须选择 Microsoft 定义的命令代码的值。 Microsoft 不能选择命令代码，并假定没有其他供应商使用的代码有冲突的用途。 它是不安全发出特定于供应商的命令，并依赖于控制器拒绝该命令，如果不了解它。 控制器无法将该命令解释为一个破坏性操作，例如更新控制器的固件。

供应商必须通过在控制器以外的方法进行通信所选的值。 Microsoft 不会指定如何获取所选的代码。

|HCI 命令|描述|
|---|---|
|[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features) | HCI_VS_MSFT_Read_Supported_Features 提供描述其中一个位图 Microsoft 定义功能在控制器支持，并指定 Microsoft 定义的事件返回的控制器的前缀。|
|[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi) | HCI_VS_MSFT_Monitor_Rssi 请求在控制器启动监视指定的连接，测量的链接 RSSI 并生成连接的测量的链接 RSSI 转到指定范围之外时发生的事件。|
|[HCI_VS_MSFT_Cancel_Monitor_Rssi](#hci_vs_msft_cancel_monitor_rssi) |HCI_VS_MSFT_Cancel_Monitor_Rssi 取消以前颁发 HCI_VS_MSFT_Monitor_Rssi 命令。|
|[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement) | HCI_VS_MSFT_LE_Monitor_Advertisement 请求在控制器启动监视播发的处于指定 RSSI 范围内并且还满足其他要求。|
|[HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement](#hci_vs_msft_le_cancel_monitor_advertisement) | HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 取消以前颁发 HCI_VS_MSFT_LE_Monitor_Advertisement 命令。|
[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable) | HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 设置播发筛选器的状态。|
|[HCI_VS_MSFT_Read_Absolute_RSSI](#hci_vs_msft_read_absolute_rssi) | HCI_VS_MSFT_Read_Absolute_RSSI 从控制器中读取 b R/edr 规范连接的绝对收到信号强度指示 (RSSI) 值。|

### <a name="notifying-windows-bluetooth-stack-of-the-vendor-specific-command-code"></a>通知 Windows Bluetooth 堆栈的供应商特定的命令代码

Windows Bluetooth 堆栈从注册表项读取特定于供应商的命令代码。

VsMsftOpCode 注册表项的 REG_DWORD 类型，因此关键数据的供应商特定的操作码。

VsMsftOpCode 项的注册表路径是：

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Device instance path>\Device Parameters\VsMsftOpCode

此示例命令从命令行添加注册表值。

```cpp
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Device instance path>\Device Parameters" /v VsMsftOpCode /t REG_DWORD /d <Vendor specific command code>
```

### <a name="using-inf-to-set-the-vsmsftopcode-registry-key"></a>使用 INF 设置 VsMsftOpCode 注册表项

此外可以通过 INF 文件中添加特定于供应商的命令代码。 此示例演示如何以及在何处添加供应商特定的命令代码，以便自动添加到注册表。

```cpp
[radio.NTamd64.HW]
AddReg=radio.NTamd64.HW.AddReg
[radio.NTamd64.HW.AddReg]
HKR,,"VsMsftOpCode",0x00010001,<Vendor Specific Opcode>
```

### <a name="microsoft-defined-hci-command-and-subcommands"></a>Microsoft 定义的 HCI 命令和子命令

将控制器理解只有一个特定于 Microsoft 的 HCI 命令。 通过使用操作码扩展是特定于 Microsoft 的命令集。 Microsoft 定义 HCI 命令的第一个命令参数是指定子命令的操作码。

控制器都必须支持[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)为了支持任何其他 Microsoft HCI 子命令。 对其他命令的支持是可选的取决于 HCI_VS_MSFT_Read_Supported_Features 返回的值。 Windows 不会发送任何 Microsoft 定义的子命令，除非控制器指示对通过响应 HCI_VS_MSFT_Read_Supported_Features 子命令的支持。

### <a name="hcivsmsftreadsupportedfeatures"></a>HCI_VS_MSFT_Read_Supported_Features

HCI_VS_MSFT_Read_Supported_Features 提供描述其中一个位图 Microsoft 定义功能在控制器支持，并指定 Microsoft 定义的事件返回的控制器的前缀。

控制器应始终完成此命令与命令已完成事件结合迅速。

<table>
  <thead>
    <tr>
    <th>Command</th>
    <th>代码</th>
    <th>命令参数</th>
    <th>返回参数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>HCI_VS_MSFT_Read_Supported_Features</td>
      <td>所选择的基本代码 </td>
      <td>Subcommand_opcode</td>
      <td>
        <ul>
          <li>状态</li>
          <li>Subcommand_opcode</li>
          <li>Supported_features</li>
          <li>Microsoft_event_prefix_length</li>
          <li>Microsoft_event_prefix</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

#### <a name="commandparameters"></a>Command_parameters

**Subcommand_opcode** （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00   |  HCI_VS_MSFT_Read_Supported_Features 子命令操作码。|

#### <a name="returnparameters"></a>Return_parameters

**状态**（1 个字节）：

| 值  |  参数说明 |
|---|---|
|  0x00 |  命令成功。 |
| 0x01&#160;-&#160;0xFF  |  该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。 |

**Subcommand_opcode** （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00   |  为子命令的操作码[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)。|

**Supported_features** （8 个字节）：

| 值  |  参数说明 |
|---|---|
|0x00000000&#160;00000001  |控制器对于 b R/edr 规范连接支持的 RSSI 监视功能。 此外，在控制器支持[HCI_VS_MSFT_Read_Absolute_RSSI](#hci_vs_msft_read_absolute_rssi)读取 b R/edr 规范连接的绝对 RSSI 指标。 |
|0x00000000&#160;00000002  |控制器对于 LE 连接支持的 RSSI 监视功能。 |
|0x00000000&#160;00000004  |控制器支持 LE RSSI 监视播发。 |
|0x00000000&#160;00000008|控制器支持广告 LE 监视播发。|
|0x00000000&#160;00000010 |控制器支持验证的公共有效性 X 和 Y 坐标在曲线上期间保护简单 P-192 和 p-256 配对过程。 <br/>有关详细信息，请参阅[蓝牙核心规范错误 10734](https://www.bluetooth.org/docman/handlers/downloaddoc.ashx?doc_id=447440)。|
|0x00000000 00000020|控制器支持与其他单选活动并发执行的连续广告监视的 LE 播发。|
|0xFFFFFFFF&#160;FFFFFFF0|保留用于未来的定义位。 必须为零。|

**Microsoft_event_prefix_length** （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00&#160;-&#160;0x20|指定在返回 Microsoft 事件前缀字段中的字节数_Microsoft_event_prefix_。 这是信息的常量开头的每个 Microsoft 指定 HCI 事件的字节数。|

**Microsoft_event_prefix** （可变长度）：

| 值  |  参数说明 |
|---|---|
|事件&#160;前缀&#160;值| 常量在每个 Microsoft 定义的事件的开始处出现的情况的信息。 此信息用于将 Microsoft 定义的事件与其他自定义事件区分开来。|

### <a name="hcivsmsftmonitorrssi"></a>HCI_VS_MSFT_Monitor_Rssi

HCI_VS_MSFT_Monitor_Rssi 请求在控制器启动监视指定的连接，测量的链接 RSSI 并生成连接的测量的链接 RSSI 转到指定范围之外时发生的事件。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_Read_Supported_Features|所选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Connection_handle</li><li>RSSI_threshold_high</li><li>RSSI_threshold_low</li><li>RSSI_threshold_low_time_interval</li><li>RSSI_sampling_period</li></ul>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

控制器应通知 RSSI 值与定期生成事件的主机 (基于_RSSI_sampling_period_)。 测量的链接应 RSSI**绝对**dBm b R/edr 规范连接中的接收方信号强度值。
HCI_VS_MSFT_Monitor_Rssi 命令响应，控制器都应生成命令完成的事件与非零值的状态或状态最零，如果控制器就可以开始监视，否则。 如果状态值为非零值，应不会生成控制器[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)中对此命令的响应。
控制器应拒绝该命令，如果命令具有相同的另一个 HCI_VS_MSFT_Monitor_Rssi _Connection_handle_是未完成，或者如果指定的连接处理无效。 在控制器还可能会出于其他原因，例如资源耗尽拒绝该命令。

#### <a name="statediagram"></a>State_diagram

连接监视 RSSI 时，此状态图的控制器上显示转换状态。![状态关系图的 HCI_VS_MSFT_Monitor_Rssi](images/HCI_VS_MSFT_Monitor_Rssi_State_Diagram.png)控制器都应生成[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)时收到的 RSSI 是否大于或等于指定_RSSI_threshold范围_。 生成此事件后，控制器不应生成以指定新 HCI_VS_MSFT_Rssi_Event _RSSI_threshold_high_之前它将生成指定 RSSI HCI_VS_MSFT_Rssi_Event 已超过已低于_RSSI_threshold_low_。

当收到的 RSSI 等于或低于指定控制器应生成 HCI_VS_MSFT_Rssi_Event _RSSI_threshold_low_内的_RSSI_threshold_low_time_interval_。 生成此事件后，控制器不应生成指定 RSSI 已低于新 HCI_VS_MSFT_Rssi_Event _RSSI_threshold_low_直到 HCI_VS_MSFT_Rssi_Event 事件生成可实现：该_RSSI_threshold_high_已达到或超出。

如果_RSSI_sampling_period_是 0x01，0xFE，控制器应生成 HCI_VS_MSFT_Rssi_Event 定期每_RSSI_sampling_period_。 此事件不应包含平均值计算 RSSI _RSSI_sampling_period_。
如果_RSSI_sampling_period_是 0x00 或 0xff 内，应在控制器**不**通知定期使用 HCI_VS_MSFT_Rssi_Event 宿主。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x01   |  HCI_VS_MSFT_Monitor_Rssi 子命令操作码。|

Connection_handle （2 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x_XXXX   |  必须监视其 RSSI 连接句柄。|

RSSI_threshold_high （1 个字节）：

| 值  |  参数说明 |
|---|---|
|N_ = 范围&#160;RSSI 阈值&#160;值 |  最大的预期的 RSSI 值。 如果观察到的 RSSI 变得大于或等于此值，则控制器会生成一个事件。 为 b R/edr 规范： <ul><li>范围:-128 &lt; =  _N_ &lt;= 127 （有符号整数）</li><li>单位： dBm</li></ul>有关 LE:<ul><li>范围:-127 为 20 （有符号整数）</li><li>单位： dBm</li></ul>|

RSSI_threshold_low （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|N_ = _Low&#160;RSSI 阈值&#160;值|最小的预期的 RSSI 值。 如果观察到的 RSSI 变得，控制器会生成一个事件小于或等于此值。 为 b R/edr 规范：<ul><li>范围:-128 &lt; =  _N_ &lt;= 127 （有符号整数）</li><li>单位： dBm</li></ul>有关 LE:<ul><li>范围:-127 为 20 （有符号整数）</li><li>单位： dBm</li></ul>|

RSSI_threshold_low_time_interval （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x00|保留的值。|
|N_&#160;=&#160;0x01&#160;-&#160;0x3C|时间段 = _N_ * 1 secondThe 时间 （秒） 对其 RSSI 值应为如下_RSSI_threshold_low_之前[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)生成。

RSSI_sampling_period （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00|保留的值。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xFE|时间段 = _N_ * 100 millisecondsThe 采样间隔 （毫秒）。|
|0xFF|保留的值。|

#### <a name="returnparameters"></a>Return_parameters

状态 （1 个字节）：

| 值  |  参数说明 |
|---|---|
|  0x00 |  命令成功。 |
| 0x01&#160;-&#160;0xFF  |  该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。 |
|0x07|控制器应会返回_超出内存容量_如果它不具有足够的内存来处理命令。|
|_错误&#160;代码_| 该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。|

Subcommand_opcod （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x01|HCI_VS_MSFT_Monitor_Rssi 子命令操作码。|

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

命令完成的事件时收到 HCI_VS_MSFT_Monitor_Rssi 命令时都应立即生成控制器。 如果命令完成事件返回的状态为 0，应生成控制器[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)发生下列情况之一时。

- 通过设备观察到的 RSSI _RSSI_threshold_low_time_interval_变得比指定小于或等于_RSSI_threshold_low_值。

- 观察到的 RSSI 设备变得大于或等于指定_RSSI_threshold_high_值。

- _RSSI_sampling_period_有效且采样期已过。

控制器应执行所有必要的清理操作，如果与指定的设备的连接丢失。 在这种情况下， [HCI_VS_MSFT_Cancel_Monitor_Rssi](#hci_vs_msft_cancel_monitor_rssi)命令不会发送到控制器。

### <a name="hcivsmsftcancelmonitorrssi"></a>HCI_VS_MSFT_Cancel_Monitor_Rssi

HCI_VS_MSFT_Cancel_Monitor_Rssi 取消以前颁发[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)命令。
在控制器中对此命令的响应都应立即生成命令已完成事件。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_Cancel_Monitor_Rssi|所选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x02   |  HCI_VS_MSFT_Cancel_Monitor_Rssi 子命令操作码。|

Connection_handle （1 个八位字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x_XXXX   |  必须取消其 RSSI 连接句柄。|

#### <a name="returnparameters"></a>Return_parameters

状态 （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令成功。 |
| 0x01&#160;-&#160;0xFF  |  该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。 |

Subcommand_opcod （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x02|HCI_VS_MSFT_Cancel_Monitor_Rssi 子命令操作码。|

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

控制器应生成命令完成事件时收到 HCI_VS_MSFT_Cancel_Monitor_RSSI 命令。

### <a name="hcivsmsftlemonitoradvertisement"></a>HCI_VS_MSFT_LE_Monitor_Advertisement

HCI_VS_MSFT_LE_Monitor_Advertisement 请求在控制器启动监视播发的处于指定 RSSI 范围内并且还满足以下条件之一：

- 指定的模式可以匹配到已接收的播发的包。
- 可以与已接收的播发 packe 匹配指定的 UUID
- 指定标识解析键 (IRK) 可以用于解决播发数据包产生的设备的专用地址。
- 指定的蓝牙地址可以匹配到已接收的播发的包。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Advertisement|所选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状态</li><li>Subcommand_opcode<li>Monitor_handle</li></ul>|

控制器应在响应此命令生成命令完成事件。 状态值应否则设置为非零值的状态或如果控制器就可以开始监视，则为零。
如果该控制器不支持 RSSI 监视 LE 播发，则它应忽略_RSSI_threshold_high_， _RSSI_threshold_low_， _RSSI_threshold_low_time_interval_，并_RSSI_sampling_period_参数值。

#### <a name="statediagram"></a>State_diagram

监视 RSSI 的播发时，此状态图的控制器上显示转换状态。 ![HCI_VS_MSFT_LE_Monitor_Advertisement 的状态图](images/HCI_VS_MSFT_LE_Monitor_Advertisement_State_Diagram.png)。 控制器应传播到主机的第一个播发数据包，仅当接收到的 RSSI 是否大于或等于_RSSI_threshold_high_为特定的设备。 生成控制器应[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)与_Monitor_state_设置为 1 并_Monitor_handle_设置为此的句柄_条件_，用于通知宿主控制器正在监视的此特定设备_条件_。
控制器应停止监视_条件_如果接收到播发的 RSSI 等于或低于_RSSI_threshold_low_转移_RSSI_threshold_low_interval_为特定设备。 生成控制器应[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)与_Monitor_state_设置为 0，用于通知宿主控制器已停止监视特定设备_条件_。 在控制器指定与 HCI_VS_MSFT_LE_Monitor_Device_Event 后_Monitor_state_设置为 0，控制器应不允许将进一步播发数据包流到设备的主机，直到控制器通知的主机需要为特定设备 RSSI 或更高版本_RSSI_threshold_high_为特定设备_条件_。
此外，应生成控制器[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)与_Monitor_state_设置为 0，用于通知宿主控制器已停止监视的设备_条件_如果指定_RSSI_threshold_low_time_interval_到期且无需从设备接收任何广告数据包。 如果该控制器监视针对特定条件的设备，以下语句为 true。

- 如果 RSSI_sampling_period_ 设置为 0xFF，控制器应不允许进一步通告数据包流到的设备的主机_条件_直到控制器具有通知主机特定设备的 RSSI已低于_RSSI_threshold_low_有关_RSSI_threshold_low_time_interval_此特定设备_条件_。 此通知通过生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)与_Monitor_state_设置为 0。
- 如果_RSSI_sampling_period_设置为 0x0，控制器应为此传播到设备的主机的所有接收到的播发数据包_条件_除非以前接收的控制器[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令_启用_设为 0x00。 控制器应传播到主机的播发数据包，即使收到的 RSSI 是否小于或等于_RSSI_threshold_low_只要_RSSI_threshold_low_time_interval_是否未过期为此特定的设备_条件_。 此播发数据包的 RSSI 值必须是已接收播发的 RSSI 值。

如果_RSSI_sampling_period_是 0x01，0xFE，控制器应传播到主机的通告数据包每_RSSI_sampling_period_指定除非以前的控制器收到[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令_启用_设为 0x00。 为播发指定的 RSSI 值应在此采样间隔期间收到的 RSSI 值的平均值。 如果控制器未在采样期间收到的播发数据包，它应不会传播到主机播发。 可能的_RSSI_sampling_period_是小于_RSSI_threshold_low_time_interval_和过程中接收到的所有播发_RSSI_sampling_period_具有以下 RSSI _RSSI_threshold_low_。 控制器仍应传播此采样间隔内收到的 RSSI 值与平均值的播发。

如果控制器之前收到[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令_启用_设置为 0x00，采样期间计时器会停止。 示例，请参阅：有关详细信息的采样期间使用的筛选器的 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable。
如果控制器收到来自同一设备的非重复通告数据包，它应匹配每个播发数据包与存储在控制器上的条件。

如果在控制器从多个条件相匹配的设备接收播发数据包，则应生成控制器[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)每个_条件_匹配，与_Monitor_handle_设置为_条件_匹配。

如果控制器无法监视范围相匹配的所有设备的 RSSI 值_条件_，它将使监视可使用任意数量的设备。 决定应监视哪些设备将取决于已接收播发的 RSSI 值。 控制器应监视设备具有更大的接收到的信号强度。

如果控制器已通知主机有关特定设备 (_A_) 和其所监视设备达到最大硬件容量要求，并且如果另一台设备 (_B_) 然后进入具有较高的 RSSI 值的范围控制器应通知宿主，它已停止监视设备 (_A_) 通过生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)与_Monitor_state_设置为 0。 控制器也应会生成与 HCI_VS_MSFT_LE_Monitor_Device_Event _Monitor_state_设置为 1，用于通知宿主的设备 (_B_) 现在受监视。

#### <a name="conditiontypeandconditionparameters"></a>Condition_type_and_Condition_parameters

_Condition_type_参数指定是否_条件_参数指定的模式、 UUID、 IRK 或 BD_ADDR。
如果_Condition_type_参数指定一种模式，_条件_包含两个部分包含的模式中存在数_条件_，和模式的数据。![模式条件的数据布局](images/HCI_VS_MSFT_LE_Monitor_Advertisement_Conditions.png)
_数的模式_指定需要匹配的模式的数量。

_模式数据_采用以下格式。

- _长度_指定此模式的长度包括的数据类型和启动模式的字节。
- _AD 类型_指定 AD 类型字段。
- _模式的起始位置_指定紧跟 AD 类型的模式的起始字节位置。
- _模式_的大小为 (_长度_-0x2) 和要为指定类型的 AD 中的播发数据包中指定的起始字节匹配的模式。

如果有多个指定的模式，控制器应确保该模式中至少一个与匹配接收到的播发。

如果_Condition_type_参数指定一个 UUID_条件_参数包含一个 UUID 类型和 UUID。 UUID 类型指定 UUID 是 16 位、 32 位或 128 位。 控制器应分析播发数据包的服务 UUID，检查指定的 UUID。 如果 UUID 类型定义为 0x01，控制器应分析的 16 位服务 Uuid 不完整的列表以及服务 UUID AD 类型中指定的 16 位服务 Uuid 的完整列表。 如果 UUID 类型定义为 0x02，控制器应分析不完整的 32 位服务 Uuid 列表和服务 UUID AD 类型中指定的 32 位 Uuid 的完整列表。 如果指定的 UUID 类型，0x03 控制器应分析不完整的 128 位服务 Uuid 列表和 128 位服务 Uuid 服务 UUID AD 类型中指定的完整列表。

如果_Condition_type_参数指定 IRK_条件_参数包含 IRK。

如果_Condition_type_参数指定蓝牙地址_条件_参数包含的地址类型和 BD_ADDR。

控制器应保留监视基于的条件，即使启用了扫描 （主动或被动）。
启用 active 扫描后，筛选器匹配的播发的扫描响应应传播到主机。

如果已禁用筛选器时，控制器仍会收到 HCI_VS_MSFT_LE_Monitor_Advertisement 命令 (由于以前接收[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令与_启用_设为 0x00)，如果它可以但将其设置为禁用状态，在控制器应接受命令。
在控制器还可能会由于等资源耗尽其他原因而拒绝该命令。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x03   |  HCI_VS_MSFT_LE_Monitor_Advertisement 子命令操作码。|

RSSI_threshold_high （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|高 RSSI 阈值|  最大的预期的 RSSI 值。 如果观察到的 RSSI 变得大于或等于此值，则控制器会生成一个事件。 有关 LE:<ul><li>范围:-127 为 20 （有符号整数）</li><li>单位： dBm</li></ul>|

RSSI_threshold_low （1 个字节）：

| 值  |  参数说明 |
|---|---|
|低 RSSI 阈值|最小的预期的 RSSI 值。 如果观察到的 RSSI 变得，控制器会生成一个事件小于或等于此值。 有关 LE:<ul><li>范围:-127 为 20 （有符号整数）</li><li>单位： dBm</li></ul>|

RSSI_threshold_low_time_interval （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00|保留的值。|
|N_&#160;=&#160;0x01&#160;-&#160;0x3C|时间段 = _N_ * 1 秒。 时间 （秒） 对其 RSSI 值应为如下_RSSI_threshold_low_之前[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)生成。

RSSI_sampling_period （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x00|保留的值。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xFE|时间段 = _N_ * 100 毫秒。 采样间隔 （毫秒）。|
|0xFF|控制器应不会传播到主机的已接收任何的播发。|

Condition_type （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x01|条件是具有播发要匹配的模式。|
|0x02|条件为 UUID 类型和 UUID。|
|0x03|条件为 IRK 的分辨率。|
|0x04|条件为蓝牙地址。|

条件：为条件适用的字段取决于 Condition_type 的值。 请参阅 Condition_type 和条件参数部分，以了解详细信息。

Number_of_patterns （1 个字节）：

|值 | 参数说明|
|---|---|
|0xXX| 模式 Pattern_data 参数中指定的数量。|

Pattern_data (> 3 个八位字节):

|值 | 参数说明|
|---|---|
|长度|此模式的长度。|
|数据类型| 播发部分的数据类型。 蓝牙分配数字文档中列出了值。|
|起始字节| 要为指定的数据类型匹配的模式的起始位置。|
|模式| 要进行模式匹配 （长度 – 0x2 字节的大小）。|

UUID_type （1 个字节）：

|ReplTest1 | 参数说明|
|---|---|
|0x01| UUID 是 16 位服务。|
|0x02| UUID 是 32 位服务。|
|0x03| UUID 是 128 位服务。|

UUID （2、 4 或 16 个八位字节）：

|ReplTest1 | 参数说明|
|---|---|
|0xXXXX| <p>如果 UUID_type 0x01 2 个字节。<p><p>如果 UUID_type 0x02 4 个字节。</p><p>如果 UUID_type 0x03 16 个字节。</p>|

IRK （16 个八位字节）：

| ReplTest1  |  参数说明 |
|---|---|
|<p>0xXXXXXXXX XXXXXXXX</p><p>XXXXXXXX XXXXXXXX</p>|要用来解决的专用地址 IRK。|

Address_type （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00| 公共设备地址。|
|0x01| 随机设备地址。|
|0x02 - 0xFF| 供将来使用的保留的值。|

Address_type （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0xXXXXXXXXXXXX|要监视的设备的蓝牙地址。|

#### <a name="returnparameters"></a>Return_parameters

状态 （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令成功。 |
|0x07|如果不具有足够的内存来处理该命令在控制器应会返回超出内存容量。|
| 错误代码  |  该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。 |

Subcommand_opcode （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x03| HCI_VS_MSFT_LE_Monitor_Advertisement 子命令操作码。 |

Monitor_handle （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x00 - 0xFF|此规则句柄。 此句柄作为 HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 的参数用于取消监视播发。 此参数才有效状态为 0x00。|

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

当收到 HCI_VS_MSFT_LE_Monitor_Advertisement 命令时，控制器都应生成命令完成事件。

### <a name="hcivsmsftlecancelmonitoradvertisement"></a>HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement

HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 取消以前颁发[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement|所选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Monitor_handle</li>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

在控制器中对此命令的响应都应立即生成命令已完成事件。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x04   |  HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 子命令操作码。|

Connection_handle （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0xXX| 正在取消的筛选器句柄。|

#### <a name="returnparameters"></a>Return_parameters

状态 （1 个字节）：

| 值  |  参数说明 |
|---|---|
|  0x00 |  命令成功。 |
|0x07|如果不具有足够的内存来处理该命令在控制器应会返回超出内存容量。|
| 错误代码  |  该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。 |

Subcommand_opcode （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x04| HCI_VS_MSFT_LE_Cancel_Monitor_Adver 子命令操作码。 |

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

控制器应生成命令完成事件时收到 HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 命令。

### <a name="hcivsmsftlesetadvertisementfilterenable"></a>HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable

HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 设置播发筛选器的状态。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable|所选择的基本代码 |<ul><li>Subcommand_opcode</li><li>启用</li>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

如果_启用_设置为 0x00，控制器应传播到基于现有列入允许列表设置主机接收到的播发。 控制器应持续监视的设备的当前正在监视并生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)与_Monitor_state_如果设备不能再设置为 0被监视。 控制器应生成与 HCI_VS_MSFT_LE_Monitor_Device_Event _Monitor_state_设置为 1，如果正在监视的新设备。 主机可能会发出与 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable_启用_设置为 0x01 以重新启用所有筛选器条件。

如果_启用_设置为 0x01，此命令将启用设置了以前颁发的所有筛选器[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令。 如果它不会切换筛选器状态，在控制器应拒绝 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令：

- 控制器应拒绝与 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令_启用_设置为 0x01，如果它以前已收到与 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令_启用_设置为 0x01。
- 控制器应拒绝与 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令_启用_它以前已收到与 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令的情况下设置为 0x00 _启用_设为 0x00。

播发筛选器的默认状态应为。 此状态相当于以前接收 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令与控制器_启用_设为 0x00。
在控制器中对此命令的响应都应立即生成命令已完成事件。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x05|  HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 子命令操作码。|

启用 （1 个字节）：

| 值  |  参数说明 |
|---|---|
|0x00| 还原到当前的白名单行为，但继续监视设备基于从 _Condition_s [HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令。|
|0x01|启用在控制器上的所有颁发的 HCI_VS_MSFT_LE_Monitor_Advertisement 命令。|

#### <a name="returnparameter"></a>Return_parameter

状态 （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x00|命令成功。|
|0x0C|控制器应会返回_命令不允许_如果在控制器拒绝了命令，因为它以前看到 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令_启用_设置为此命令相同的值。|
|错误&#160;代码|该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。|

Subcommand_opcode （1 个字节）：

|值|参数说明|
|---|---|
|0x05|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 子命令操作码。|

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

控制器应生成命令完成事件时收到 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令。

#### <a name="hcivsmsftreadabsoluterssi"></a>HCI_VS_MSFT_Read_Absolute_RSSI

读取 HCI_VS_MSFT_Read_Absolute_RSSI**绝对**b R/edr 规范连接从控制器接收信号强度指示 (RSSI) 值。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_Read_Absolute_RSSI|所选择的基本代码 |<ul><li>Subcommand_opcode</li><li>句柄</li>|<ul><li>状态</li><li>Subcommand_opcode</li><li>句柄</li><li>RSSI</li></ul>|

作为命令和返回参数来标识正在读取其 RSSI ACL 连接提供连接句柄。 RSSI 度量值是**绝对**dBm 为 6 dB 准确度在接收方信号强度。 如果无法读取 RSSI，RSSI 度量值应设置为 127。
控制器应始终完成此命令与命令已完成事件结合迅速。

#### <a name="commandparameters"></a>Command_parameters

Subcommand_opcode （1 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x06|  HCI_VS_MSFT_Read_Absolute_RSSI 子命令操作码。|

句柄 （2 个字节）：

| ReplTest1  |  参数说明 |
|---|---|
|0x_XXXX_|其 RSSI 必须要读取的 b R/edr 规范连接句柄。|

#### <a name="returnparameters"></a>Return_parameters

状态 （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x00|命令成功。|
|0x01 - 0xFF|该命令失败。 请参阅_错误代码_蓝牙核心规范中有关详细信息。|

Subcommand_opcode （1 个字节）：

|值|参数说明|
|---|---|
|0x06|HCI_VS_MSFT_Read_Absolute_RSSI 子命令操作码。|

句柄 （2 个字节）：

|值|参数说明|
|---|---|
|0xXXXX| 读取其 RSSI b R/edr 规范连接句柄。|

RSSI （1 个字节）：

|     值      |                                                  参数说明                                                   |
|----------------|--------------------------------------------------------------------------------------------------------------------------|
| N = RSSI 值 | B R/edr 规范连接 RSSI 值。<ul><li>范围:-128 &lt; =  *N* &lt;= 127 （有符号整数）</li><li>单位： dBm</li> |

#### <a name="eventsgeneratedunlessmaskedaway"></a>Events_generated__unless_masked_away

控制器应生成 HCI_VS_MSFT_Read_Absolute_RSSI 命令完成后的命令完成事件。

## <a name="microsoft-defined-bluetooth-hci-events"></a>Microsoft 定义的蓝牙 HCI 事件

所有 Microsoft 定义蓝牙 HCI 事件供应商定义的事件，然后使用事件代码 0xFF。 Microsoft 事件的事件数据始终以开头的字节将 Microsoft 定义的事件与其他供应商定义的事件区分开来的常量字符串。 定义由控制器实现者和响应中返回的长度和值的常量字符串[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)。

|HCI 事件|描述|
|---|---|
|[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)|HCI_VS_MSFT_RSSI_Event 指示[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)命令是否已完成。|
|[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)|HCI_VS_MSFT_LE_Monitor_Device_Event 指示控制器已启动或停止监视蓝牙 LE 设备。|

### <a name="hcivsmsftrssievent"></a>HCI_VS_MSFT_RSSI_Event

HCI_VS_MSFT_RSSI_Event 指示[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)命令是否已完成。
如果_状态_参数为零，该命令完成，因为远程设备的 RSSI 值更改为指定范围之外的值。 如果_状态_参数为非零，该命令完成，因为不再可以监视连接的 RSSI 值。

|Event|事件代码|Microsoft 事件代码|事件参数|
|---|---|---|---|
|HCI_VS_MSFT_RSSI_Event|0xFF|0x01|<p>Event_prefix</p><p>Microsoft_event_code</p><p>状态</p><p>Connection_handle</p><p>RSSI</p>

#### <a name="eventparameters"></a>Event_parameters

Event_prefix （变量大小）：

|ReplTest1|参数说明|
|---|---|
|事件前缀|标记为 Microsoft 定义此事件的事件前缀。 大小和值是所返回的[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)命令。|

Microsoft_event_code （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x01|HCI_VS_MSFT_RSSI_Event 事件代码。|

状态 （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x00|成功。 连接的 RSSI 值已满足以下条件之一。<ul><li>RSSI 达到或超出_RSSI_threshold_high_。</li><li>RSSI 达到或下降到低于_RSSI_threshold_low_转移_RSSI_threshold_low_time_interval_秒。</li><li>_RSSI_sampling_period_已过期并生成该事件用于通知宿主 RSSI 值。</li></ul>|
|0x01&#160;-&#160;0xFF|失败。 连接的 RSSI 值可以不再进行监视。 错误代码通常是介绍基础的 ACL 连接已断开的原因代码之一。|

Connection_handle （2 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x_XXXX_|要监视其 RSSI 的连接句柄。|

RSSI （1 个字节）：

|值|参数说明|
|---|---|
|_N_ = _RSSI&#160;值_|测量的链接连接的 RSSI 值。 为 b R/edr 规范：<ul><li>范围:-128 &lt; =  _N_ &lt;= 127 （有符号整数）</li><li>单位： dBm</li></ul>有关 LE:<ul><li>范围:-127 为 20 （有符号整数）</li><li>单位： dBm</li></ul>|

### <a name="hcivsmsftlemonitordeviceevent"></a>HCI_VS_MSFT_LE_Monitor_Device_Event

HCI_VS_MSFT_LE_Monitor_Device_Event 指示控制器已启动或停止监视蓝牙 LE 设备。

如果_Monitor_state_参数值为 1，控制器开始监视指定 BD_ADDR 的蓝牙设备。 如果_Monitor_state_参数值为 0，则该控制器已停止监视指定 BD_ADDR 的蓝牙设备。

|Event|事件代码|Microsoft 事件代码|事件参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Device_Event|0xFF|0x02|<p>Event_prefix</p><p>Microsoft_event_code</p><p>Address_type</p><p>BD_ADDR</p><p>Monitor_handle</p><p>Monitor_state</p>

控制器不会生成与 HCI_VS_MSFT_LE_Monitor_Device_Event _Monitor_state_参数设置为 0，如果没有具有已生成具有 HCI_VS_MSFT_LE_Monitor_Device_Event _Monitor_state_设置为 1。

#### <a name="eventparameters"></a>Event_parameters

Event_prefix （变量大小）：

|ReplTest1|参数说明|
|---|---|
|事件前缀|标记为 Microsoft 定义此事件的事件前缀。 大小和值是所返回的[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)命令。

Microsoft_event_code （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x02|HCI_VS_MSFT_LE_Monitor_Device_Event 事件代码。|

Address_type （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x00|公共设备地址。|
|0x01|随机设备地址。|
|0x02&#160;-&#160;0xFF|供将来使用的保留的值。|

BD_ADDR （6 个八位字节）：

|值|参数说明|
|---|---|
|0x_XXXXXXXXXXXX_|蓝牙设备的地址。|

Monitor_handle （1 个字节）：

|ReplTest1|参数说明|
|---|---|
|0x_XX_|为指定的筛选器的句柄[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令。|

Monitor_state （1 个字节）：

|值|参数说明|
|---|---|
|0x00|控制器已停止监视指定的设备_BD_ADDR_并_Monitor_handle_。|
|0x01|在控制器开始监视指定的设备_BD_ADDR_并_Monitor_handle_。|
