---
title: Microsoft 定义的蓝牙 HCI 命令和事件
description: 蓝牙主机控制器接口 (HCI) 指定主机和蓝牙无线电控制器之间的所有交互。
ms.assetid: 68E34B92-155B-401E-8D90-5BD1AF036B4D
ms.date: 02/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 400fdb42155f468a03c2570cfa295f269334f44c
ms.sourcegitcommit: 2c3b8e0ea0e75b72067d2e22dc530390bc19b11e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2019
ms.locfileid: "63328227"
---
# <a name="microsoft-defined-bluetooth-hci-extensions"></a>Microsoft 定义的蓝牙 HCI 扩展

蓝牙主机控制器接口 (HCI) 指定主机和蓝牙无线电控制器之间的所有交互。 Bluetooth 规范允许供应商定义的 HCI 命令和事件启用主机和控制器之间的非标准化交互。 Microsoft 定义了特定于供应商的 HCI 命令和 Windows 使用的事件。 蓝牙控制器实现者可以使用这些扩展来实现特殊功能。

## <a name="requirements"></a>要求

适用于桌面版 (家庭版、专业版、企业版和教育版)、Windows 10 移动版和更高版本的 Windows 10。

## <a name="microsoft-defined-hci-commands"></a>Microsoft 定义的 HCI 命令

蓝牙 HCI 命令由16位命令代码标识。 蓝牙组织定义0x0000 到0xFBFF 范围内的值。 供应商定义0xFC00 到0xFFFF 范围内的值, 允许1024个可能不同的供应商分配的命令代码。

供应商必须选择 Microsoft 定义的命令代码的值。 Microsoft 无法选择命令代码, 并假设没有其他供应商出于冲突目的使用此代码。 发出特定于供应商的命令不安全, 如果不了解该命令, 则依赖于控制器拒绝该命令。 控制器可以将命令解释为破坏性操作, 例如更新控制器的固件。

供应商必须通过控制器之外的方法传达所选值。 Microsoft 不指定如何获取所选代码。

|HCI 命令|描述|
|---|---|
|[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features) | HCI_VS_MSFT_Read_Supported_Features 提供一个位图, 用于描述控制器支持的 Microsoft 定义功能, 并为控制器返回的 Microsoft 定义的事件指定前缀。|
|[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi) | HCI_VS_MSFT_Monitor_Rssi 请求控制器开始监视指定连接的已测量链接 RSSI, 并在连接的度量链接 RSSI 超出指定边界时生成事件。|
|[HCI_VS_MSFT_Cancel_Monitor_Rssi](#hci_vs_msft_cancel_monitor_rssi) |HCI_VS_MSFT_Cancel_Monitor_Rssi 取消以前发布的 HCI_VS_MSFT_Monitor_Rssi 命令。|
|[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement) | HCI_VS_MSFT_LE_Monitor_Advertisement 请求控制器开始监视位于指定 RSSI 范围内并且还满足其他要求的播发。|
|[HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement](#hci_vs_msft_le_cancel_monitor_advertisement) | HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 取消以前发布的 HCI_VS_MSFT_LE_Monitor_Advertisement 命令。|
[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable) | HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 设置播发筛选器的状态。|
|[HCI_VS_MSFT_Read_Absolute_RSSI](#hci_vs_msft_read_absolute_rssi) | HCI_VS_MSFT_Read_Absolute_RSSI 从控制器读取 BR/EDR 连接的绝对接收信号强度指示 (RSSI) 值。|

### <a name="notifying-windows-bluetooth-stack-of-the-vendor-specific-command-code"></a>向 Windows 蓝牙堆栈提供特定于供应商的命令代码

Windows 蓝牙堆栈从注册表项中读取特定于供应商的命令代码。

VsMsftOpCode 注册表项具有类型的 REG_DWORD, 密钥数据是特定于供应商的操作码。

VsMsftOpCode 项的注册表路径为:

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<设备实例路径 > \Device Parameters\VsMsftOpCode

此示例命令从命令行添加注册表值。

```cpp
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\<Device instance path>\Device Parameters" /v VsMsftOpCode /t REG_DWORD /d <Vendor specific command code>
```

### <a name="using-inf-to-set-the-vsmsftopcode-registry-key"></a>使用 INF 设置 VsMsftOpCode 注册表项

还可以通过 INF 文件添加特定于供应商的命令代码。 此示例演示如何以及在何处添加特定于供应商的命令代码, 以便将其自动添加到注册表中。

```cpp
[radio.NTamd64.HW]
AddReg=radio.NTamd64.HW.AddReg
[radio.NTamd64.HW.AddReg]
HKR,,"VsMsftOpCode",0x00010001,<Vendor Specific Opcode>
```

### <a name="microsoft-defined-hci-command-and-subcommands"></a>Microsoft 定义的 HCI 命令和子命令

控制器知道只有一个特定于 Microsoft 的 HCI 命令。 Microsoft 专用命令集通过使用操作码进行扩展。 Microsoft 定义的 HCI 命令的第一个命令参数是用于指定子命令的操作码。

控制器必须支持[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features) , 以便支持任何其他 Microsoft HCI 子命令。 支持其他命令是可选的, 具体取决于 HCI_VS_MSFT_Read_Supported_Features 返回的值。 Windows 不会发送任何 Microsoft 定义的子命令, 除非控制器通过对 HCI_VS_MSFT_Read_Supported_Features 的响应来指示支持子命令。

### <a name="hci_vs_msft_read_supported_features"></a>HCI_VS_MSFT_Read_Supported_Features

HCI_VS_MSFT_Read_Supported_Features 提供一个位图, 用于描述控制器支持的 Microsoft 定义功能, 并为控制器返回的 Microsoft 定义的事件指定前缀。

控制器始终应始终使用命令完成事件立即完成此命令。

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
      <td>选择的基本代码 </td>
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

#### <a name="command_parameters"></a>Command_parameters

**Subcommand_opcode**(1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|0x00   |  HCI_VS_MSFT_Read_Supported_Features 的子命令操作码。|

#### <a name="return_parameters"></a>Return_parameters

**状态**(1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令已成功。 |
| 0x01&#160;-&#160;0xff  |  命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。 |

**Subcommand_opcode**(1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|0x00   |  [HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)的子命令操作码。|

**Supported_features**(8 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|0x00000000&#160;00000001  |控制器支持 BR/EDR 连接的 RSSI 监视功能。 此外, 控制器还支持[HCI_VS_MSFT_Read_Absolute_RSSI](#hci_vs_msft_read_absolute_rssi)读取 BR/EDR 连接的绝对 RSSI 指标。 |
|0x00000000&#160;00000002  |控制器支持 LE 连接的 RSSI 监视功能。 |
|0x00000000&#160;00000004  |控制器支持 RSSI 监视 LE 播发。 |
|0x00000000&#160;00000008|控制器支持 LE 播发的播发监视。|
|0x00000000&#160;00000010 |控制器支持在 P-192 和 P-256 的安全简单配对过程中验证曲线上公共 X 和 Y 坐标的有效性。 <br/>有关详细信息, 请参阅[蓝牙核心规范错误 10734](https://www.bluetooth.org/docman/handlers/downloaddoc.ashx?doc_id=447440)。|
|0x00000000 00000020|控制器支持与其他无线电活动并发执行的 LE 广告的持续广告监视。|
|0xFFFFFFFF&#160;FFFFFFF0|保留以供将来定义的位。 必须为零。|

**Microsoft_event_prefix_length**(1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|0x00&#160;-&#160;0x20|在返回的_Microsoft_event_prefix_中指定的 Microsoft 事件前缀字段中的字节数。 这是每个 Microsoft 指定的 HCI 事件开始时的常量信息的字节数。|

**Microsoft_event_prefix**(可变长度):

| ReplTest1  |  参数说明 |
|---|---|
|事件&#160;前缀&#160;值| 要在每个 Microsoft 定义事件开始时预期的常量信息。 此信息用于将 Microsoft 定义的事件与其他自定义事件区分开来。|

### <a name="hci_vs_msft_monitor_rssi"></a>HCI_VS_MSFT_Monitor_Rssi

HCI_VS_MSFT_Monitor_Rssi 请求控制器开始监视指定连接的已测量链接 RSSI, 并在连接的度量链接 RSSI 超出指定边界时生成事件。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_Read_Supported_Features|选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Connection_handle</li><li>RSSI_threshold_high</li><li>RSSI_threshold_low</li><li>RSSI_threshold_low_time_interval</li><li>RSSI_sampling_period</li></ul>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

控制器应使用定期生成的事件 (基于_RSSI_sampling_period_) 通知主机 RSSI 值。 度量的链接 RSSI 应为 BR/EDR 连接的**绝对**接收方信号强度值, 单位为 dBm。
为响应 HCI_VS_MSFT_Monitor_Rssi 命令, 如果控制器可以开始监视, 则控制器应生成状态为等于的命令完成事件, 否则将生成非零状态。 如果 status 值为非零值, 则控制器不应生成[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)来响应此命令。
如果具有相同_Connection_handle_的另一个 HCI_VS_MSFT_Monitor_Rssi 命令未完成, 或指定的连接句柄无效, 则控制器应拒绝此命令。 控制器还可以出于其他原因 (例如资源耗尽) 拒绝命令。

#### <a name="state_diagram"></a>State_diagram

此状态图显示了监视连接的 RSSI 时控制器上的转换状态。HCI_VS_MSFT_Monitor_Rssi 的状态关系图: 当收到的 Rssi 大于或等于指定的_RSSI_threshold_high_时, 控制器应生成[HCI_VS_MSFT_Rssi_Event。](#hci_vs_msft_rssi_event) ![](images/HCI_VS_MSFT_Monitor_Rssi_State_Diagram.png) 此事件生成后, 控制器不会生成新的 HCI_VS_MSFT_Rssi_Event, 以指定已超过_RSSI_threshold_high_ , 直到生成指定 Rssi_的 HCI_VS_MSFT_Rssi_Event 为止RSSI_threshold_low_。

当收到的 RSSI 等于或低于指定的_RSSI_threshold_low_时, 控制器应生成 HCI_VS_MSFT_Rssi_Event。 此事件生成后, 控制器不会生成新的 HCI_VS_MSFT_Rssi_Event, 以指定 RSSI 已低于_RSSI_threshold_low_ , 直到生成 HCI_VS_MSFT_Rssi_Event 事件, 才能指定_RSSI__ 已达到或超过了 threshold_high。

如果_RSSI_sampling_period_介于0X01 和0xFE 之间, 则控制器应定期生成每个_RSSI_sampling_period_的 HCI_VS_MSFT_Rssi_Event。 此事件应包含通过_RSSI_sampling_period_计算的 RSSI 的平均值。
如果_RSSI_sampling_period_为0X00 或 0xff, 控制器**不**应定期通过 HCI_VS_MSFT_Rssi_Event 通知主机。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x01   |  HCI_VS_MSFT_Monitor_Rssi 的子命令操作码。|

Connection_handle (2 个字节):

| ReplTest1  |  参数说明 |
|---|---|
|0x_XXXX   |  必须监视其 RSSI 的连接的句柄。|

RSSI_threshold_high (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|N_ = _High&#160;RSSI 阈值&#160; |  预期的最大 RSSI 值。 如果观察到的 RSSI 将大于或等于此值, 则控制器将生成一个事件。 对于 BR/EDR: <ul><li>范围:-128 &lt; =  N&lt;= 127 (带符号整数)</li><li>Unit: dBm</li></ul>对于 LE:<ul><li>范围:-127 到 20 (带符号整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|N_ = _Low&#160;RSSI 阈值&#160;|预期的最小 RSSI 值。 如果观察到的 RSSI 小于或等于此值, 则控制器将生成一个事件。 对于 BR/EDR:<ul><li>范围:-128 &lt; =  N&lt;= 127 (带符号整数)</li><li>Unit: dBm</li></ul>对于 LE:<ul><li>范围:-127 到 20 (带符号整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low_time_interval (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00|保留值。|
|N_&#160;=&#160;&#160;0x3C&#160;|时间段 = _N_ * 1 secondThe 时间, 超过此时间后, RSSI 值应低于_RSSI_threshold_low_ , 然后才能生成[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event) 。

RSSI_sampling_period (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00|保留值。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xFE|时间段 = _N_ * 100 millisecondsThe 采样间隔 (毫秒)。|
|0xFF|保留值。|

#### <a name="return_parameters"></a>Return_parameters

状态 (1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令已成功。 |
| 0x01&#160;-&#160;0xff  |  命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。 |
|0x07|如果控制器没有足够的内存来处理该命令, 则控制器应返回_内存容量_。|
|_错误&#160;代码_| 命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。|

Subcommand_opcod (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x01|HCI_VS_MSFT_Monitor_Rssi 的子命令操作码。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

接收到 HCI_VS_MSFT_Monitor_Rssi 命令后, 控制器应立即生成命令完成事件。 如果命令完成事件返回的状态为 0, 则当发生以下情况之一时, 控制器应生成[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event) 。

- 设备上通过_RSSI_threshold_low_time_interval_观测到的 RSSI 将等于或小于指定的_RSSI_threshold_low_值。

- 设备观察到的 RSSI 将大于或等于指定的_RSSI_threshold_high_值。

- _RSSI_sampling_period_是有效的, 采样期限已过期。

如果与指定设备的连接丢失, 控制器应执行所有必要的清理。 在这种情况下, 不会将[HCI_VS_MSFT_Cancel_Monitor_Rssi](#hci_vs_msft_cancel_monitor_rssi)命令发送到控制器。

### <a name="hci_vs_msft_cancel_monitor_rssi"></a>HCI_VS_MSFT_Cancel_Monitor_Rssi

HCI_VS_MSFT_Cancel_Monitor_Rssi 取消以前发布的[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)命令。
控制器应立即生成命令完成事件以响应此命令。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_Cancel_Monitor_Rssi|选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x02   |  HCI_VS_MSFT_Cancel_Monitor_Rssi 的子命令操作码。|

Connection_handle (1 个字节):

| ReplTest1  |  参数说明 |
|---|---|
|0x_XXXX   |  必须取消其 RSSI 的连接的句柄。|

#### <a name="return_parameters"></a>Return_parameters

状态 (1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令已成功。 |
| 0x01&#160;-&#160;0xff  |  命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。 |

Subcommand_opcod (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x02|HCI_VS_MSFT_Cancel_Monitor_Rssi 的子命令操作码。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

接收到 HCI_VS_MSFT_Cancel_Monitor_RSSI 命令后, 控制器应生成命令完成事件。

### <a name="hci_vs_msft_le_monitor_advertisement"></a>HCI_VS_MSFT_LE_Monitor_Advertisement

HCI_VS_MSFT_LE_Monitor_Advertisement 请求控制器开始监视位于指定的 RSSI 范围内的播发, 同时满足以下条件之一:

- 指定模式可以与接收的播发数据包匹配。
- 指定的 UUID 可以与接收的播发 packe 匹配
- 指定的标识解析密钥 (IRK) 可用于解析播发数据包源自的设备的专用地址。
- 指定的蓝牙地址可与接收的播发数据包匹配。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Advertisement|选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Connection_handle</li>|<ul><li>状态</li><li>Subcommand_opcode<li>Monitor_handle</li></ul>|

控制器应生成命令完成事件以响应此命令。 如果控制器可以开始监视, 则 status 值应设置为零; 否则为非零状态。
如果控制器不支持 RSSI 监视 LE 播发, 则它应忽略_RSSI_threshold_high_、 _RSSI_threshold_low_、 _RSSI_threshold_low_time_interval_和_RSSI_sampling_period_参数值.

#### <a name="state_diagram"></a>State_diagram

此状态图显示了在监视播发的 RSSI 时控制器上的转换状态。 ![HCI_VS_MSFT_LE_Monitor_Advertisement](images/HCI_VS_MSFT_LE_Monitor_Advertisement_State_Diagram.png)的状态图。 仅当收到的 RSSI 大于或等于特定设备的_RSSI_threshold_high_时, 控制器才会将第一个播发数据包传播到主机。 控制器应生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event) , 并将_Monitor_state_设置为 1, 并将_Monitor_handle_设置为此_条件_的句柄, 以通知主机控制器正在监视此适用于_条件_的特定设备。
如果收到的播发的 RSSI 等于或低于_RSSI_threshold_low_ over _RSSI_threshold_low_interval_上的特定设备, 则控制器应停止监视_条件_。 控制器应生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event) , 并将_Monitor_state_设置为 0, 以通知主机控制器已停止监视特定设备的_条件_。 控制器指定将_Monitor_state_设置为0的 HCI_VS_MSFT_LE_Monitor_Device_Event 后, 控制器将不允许进一步的播发包流向该设备的主机, 直到控制器通知主机 RSSI对于特定设备, 特定设备的需要为或更高_RSSI_threshold_high_ 。
此外, 控制器应生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event) , 并将_Monitor_state_设置为 0, 以通知主机控制器已停止监视设备的_条件_(如果指定的_RSSI_)threshold_low_time_interval_过期, 无需从设备接收任何广告数据包。 如果控制器监视某个设备的特定条件, 则以下语句为 true。

- 如果将 RSSI_sampling_period_ 设置为 0xFF, 则控制器将不允许进一步的播发包流向设备的主机以查找_条件_, 直到控制器通知主机特定设备的 RSSI 低于对于此_条件_, 特定设备的_RSSI_threshold_low_time_interval_的 RSSI_threshold_low。 此通知是通过生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)并将_Monitor_state_设置为0来完成的。
- 如果将_RSSI_sampling_period_设置为 0x0, 则控制器应将接收到的所有播发数据包传播到该设备的主机,除非控制器之前接收到[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令,并将设置为0x00。 即使接收的 RSSI 小于或等于_RSSI_threshold_low_ , 控制器也应将广告数据包传播到主机, 前提是对于特定设备,此_条件_。 此播发数据包的 RSSI 值应为收到的播发的 RSSI 值。

如果_RSSI_sampling_period_介于0X01 和0xFE 之间, 则控制器应将播发数据包传播到指定的每个_RSSI_sampling_period_的主机, 除非控制器之前接收到[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令,并将设置为0x00。 为播发指定的 RSSI 值应为在此采样间隔期间接收到的 RSSI 值的平均值。 如果控制器未在采样期间接收到播发数据包, 则不应将播发传播到主机。 _RSSI_sampling_period_可能小于_RSSI_threshold_low_time_interval_ , 且_RSSI_sampling_period_期间收到的所有播发都在_RSSI_threshold_low_下面 RSSI。 控制器仍应传播此播发, 并将此 RSSI 值的平均值作为此采样间隔期间接收的值的平均值。

如果控制器以前收到的[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令的_Enable_设置为 0x00, 则不应停止采样期间计时器。 请参阅示例:有关详细信息, 请 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 有关采样期间的筛选器。
如果控制器从同一设备接收到不重复的播发数据包, 则它应将每个播发数据包与控制器上存储的条件匹配。

如果控制器从与多个条件匹配的设备接收播发数据包, 则控制器应为每个匹配的_条件_生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event) , 并使用_Monitor_handle_ 。设置为匹配的_条件_。

如果控制器无法监视范围内与_条件_相匹配的所有设备的 RSSI 值, 则它将保持监视尽可能多的设备。 应该监视的设备的决定取决于收到的播发的 RSSI 值。 控制器应监视收到的信号强度较高的设备。

如果控制器已向主机通知特定设备 (_a_), 并且它在最大硬件容量上监视设备, 并且如果另一个设备 (_B_) 的范围具有较高的 RSSI 值, 则控制器应通知主机已通过生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event) , 并将_Monitor_state_设置为0来停止监视设备 (_A_)。 控制器还应生成 HCI_VS_MSFT_LE_Monitor_Device_Event, 并将_Monitor_state_设置为 1, 通知主机现在正在监视设备 (_B_)。

#### <a name="condition_type_and_condition_parameters"></a>Condition_type_and_Condition_parameters

_Condition_type_参数指定_Condition_参数是指定模式、UUID、IRK 还是 BD_ADDR。
如果_Condition_type_参数指定了一个模式, 则该_条件_包含2个部分, 其中包含_条件_中存在的模式数和模式数据。模式条件数据布局](images/HCI_VS_MSFT_LE_Monitor_Advertisement_Conditions.png)
_模式数_指定需要匹配的模式数。 ![

_模式数据_具有以下格式:

- _Length_指定此模式的长度, 包括模式的数据类型和起始字节。
- _Ad 类型_指定 ad 类型字段。
- _模式的开始_指定紧随广告类型的模式的起始字节位置。
- _模式_的大小为 (_长度_为-0x2), 是从指定的起始字节到广告数据包内的指定广告类型要匹配的模式。

如果指定了多个模式, 控制器应确保至少有一种模式匹配接收的播发。

如果_Condition_type_参数指定了 uuid, 则_CONDITION_参数包含 uuid 类型和 uuid。 UUID 类型指定 UUID 是16位、32位还是128位。 控制器应分析播发数据包的服务 UUID, 以检查指定的 UUID。 如果 UUID 类型定义为 0x01, 则控制器应分析16位服务 Uuid 的不完整列表, 以及服务 UUID AD 类型中指定的16位服务 Uuid 的完整列表。 如果 UUID 类型定义为 0x02, 则控制器应分析32位服务 Uuid 的不完整列表, 以及在服务 UUID AD 类型中指定的32位 Uuid 的完整列表。 如果指定的 UUID 类型为 0x03, 则控制器应分析128位服务 Uuid 的不完整列表, 以及在服务 UUID AD 类型中指定的128位服务 Uuid 的完整列表。

如果_Condition_type_参数指定了 IRK, 则_CONDITION_参数包含 IRK。

如果_Condition_type_参数指定蓝牙地址, 则_Condition_参数将包含 Address 类型和 BD_ADDR。

控制器应根据条件保留监视, 即使启用了扫描 (主动或被动) 也是如此。
启用活动扫描时, 与筛选器匹配的播发的扫描响应应传播到主机。

如果在禁用筛选器的情况下, 控制器接收到 HCI_VS_MSFT_LE_Monitor_Advertisement 命令 (由于以前收到的[HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable](#hci_vs_msft_le_set_advertisement_filter_enable)命令, 并将 "_启用_" 设置为 0x00), 控制器应接受命令 (如果可以), 但将其设置为禁用状态。
控制器还可以出于其他原因 (例如资源耗尽) 拒绝命令。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x03   |  HCI_VS_MSFT_LE_Monitor_Advertisement 的子命令操作码。|

RSSI_threshold_high (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|高 RSSI 阈值|  预期的最大 RSSI 值。 如果观察到的 RSSI 将大于或等于此值, 则控制器将生成一个事件。 对于 LE:<ul><li>范围:-127 到 20 (带符号整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|低 RSSI 阈值|预期的最小 RSSI 值。 如果观察到的 RSSI 小于或等于此值, 则控制器将生成一个事件。 对于 LE:<ul><li>范围:-127 到 20 (带符号整数)</li><li>Unit: dBm</li></ul>|

RSSI_threshold_low_time_interval (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00|保留值。|
|N_&#160;=&#160;&#160;0x3C&#160;|时间段 = _N_ * 1 秒。 生成[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)之前, RSSI 值应低于_RSSI_threshold_low_的时间 (以秒为单位)。

RSSI_sampling_period (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00|保留值。|
|_N_&#160;=&#160;0x01&#160;-&#160;0xFE|时间段 = _N_ * 100 毫秒。 采样间隔 (毫秒)。|
|0xFF|控制器不应将任何收到的播发传播到主机。|

Condition_type (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x01|条件是必须在播发上进行匹配的模式。|
|0x02|条件为 UUID 类型和 UUID。|
|0x03|条件是 IRK 的解析。|
|0x04|条件是 Bluetooth 地址。|

状态适用于条件的字段取决于 Condition_type 的值。 有关详细信息, 请参阅 Condition_type and Condition parameters 部分。

Number_of_patterns (1 个八进制):

|ReplTest1 | 参数说明|
|---|---|
|0xXX| 在 Pattern_data 参数中指定的模式数。|

Pattern_data (> 3 个字节):

|ReplTest1 | 参数说明|
|---|---|
|长度|此模式的长度。|
|数据类型| 播发部分的数据类型。 这些值列在 "蓝牙分配的数字" 文档中。|
|开始字节| 要与指定的数据类型匹配的模式的起始位置。|
|模式| 要匹配的模式 (长度的大小–0x2 个字节)。|

UUID_type (1 个八进制):

|ReplTest1 | 参数说明|
|---|---|
|0x01| UUID 是16位服务。|
|0x02| UUID 为32位服务。|
|0x03| UUID 为128位服务。|

UUID (2 个、4个或16个八进制数):

|ReplTest1 | 参数说明|
|---|---|
|0xXXXX| <p>如果 UUID_type 为 0x01, 则为2个字节。<p><p>如果 UUID_type 为 0x02, 则为4字节。</p><p>如果 UUID_type 为 0x03, 则为16字节。</p>|

IRK (16 个字节):

| ReplTest1  |  参数说明 |
|---|---|
|<p>0xXXXXXXXX XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</p><p>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</p>|用于解析专用地址的 IRK。|

Address_type (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00| 公用设备地址。|
|0x01| 随机设备地址。|
|0x02-0xFF| 供将来使用的保留值。|

Address_type (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0xXXXXXXXXXXXX|要监视的设备的蓝牙地址。|

#### <a name="return_parameters"></a>Return_parameters

状态 (1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令已成功。 |
|0x07|如果控制器没有足够的内存来处理该命令, 则控制器应返回内存容量。|
| 错误代码  |  命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。 |

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x03| HCI_VS_MSFT_LE_Monitor_Advertisement 的子命令操作码。 |

Monitor_handle (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00-0xFF|此规则的句柄。 此句柄用作 HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 的参数以取消监视播发。 仅当状态为0x00 时, 此参数才有效。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

接收到 HCI_VS_MSFT_LE_Monitor_Advertisement 命令后, 控制器应生成命令完成事件。

### <a name="hci_vs_msft_le_cancel_monitor_advertisement"></a>HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement

HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 取消以前发布的[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement|选择的基本代码 |<ul><li>Subcommand_opcode</li><li>Monitor_handle</li>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

控制器应立即生成命令完成事件以响应此命令。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x04   |  HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 的子命令操作码。|

Connection_handle (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0xXX| 要取消的筛选器的句柄。|

#### <a name="return_parameters"></a>Return_parameters

状态 (1 个八进制数):

| ReplTest1  |  参数说明 |
|---|---|
|  0x00 |  命令已成功。 |
|0x07|如果控制器没有足够的内存来处理该命令, 则控制器应返回内存容量。|
| 错误代码  |  命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。 |

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x04| HCI_VS_MSFT_LE_Cancel_Monitor_Adver 的子命令操作码。 |

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

接收到 HCI_VS_MSFT_LE_Cancel_Monitor_Advertisement 命令后, 控制器应生成命令完成事件。

### <a name="hci_vs_msft_le_set_advertisement_filter_enable"></a>HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable

HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 设置播发筛选器的状态。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable|选择的基本代码 |<ul><li>Subcommand_opcode</li><li>启用</li>|<ul><li>状态</li><li>Subcommand_opcode</ul>|

如果 "_启用_" 设置为 0x00, 则控制器应基于现有的空白列表设置将接收的播发传播到主机。 如果设备不再受到监视, 控制器应继续监视当前正在监视的设备并生成[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event) , 并将_Monitor_state_设置为0。 如果正在监视新设备, 控制器应生成 HCI_VS_MSFT_LE_Monitor_Device_Event, 并将_Monitor_state_设置为1。 主机可能会发出 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable,并设置为0x01 来重新启用所有筛选条件。

如果_Enable_设置为 0x01, 则此命令将启用使用以前发布的[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令设置的所有筛选器。 如果控制器不切换筛选器状态, 则控制器应拒绝 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令:

- 如果控制器以前收到_启用_设置为0X01 的 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令, 则该控制器应拒绝_启用_了 Set to 0x01 的 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令。
- 如果先前接收到的 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令的_enable_设置为 0x00, 控制器应拒绝 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令, 并将_enable_设置为0x00。

播发筛选器的默认状态应为 "关闭"。 此状态等效于先前接收 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令并将 "_启用_" 设置为0x00 的控制器。
控制器应立即生成命令完成事件以响应此命令。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x05|  HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 的子命令操作码。|

启用 (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x00| 恢复为当前的白名单行为, 但根据[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令中的 _Condition_s 继续监视设备。|
|0x01|在控制器上启用所有发出的 HCI_VS_MSFT_LE_Monitor_Advertisement 命令。|

#### <a name="return_parameter"></a>Return_parameter

状态 (1 个八进制数):

|ReplTest1|参数说明|
|---|---|
|0x00|命令已成功。|
|0x0C|控制器拒绝命令时, 控制器将不_允许返回命令_, 因为它以前看到了 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令, 并将 "_启用_" 设置为与此命令相同的值。|
|错误&#160;代码|命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。|

Subcommand_opcode (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x05|HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 的子命令操作码。|

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

接收到 HCI_VS_MSFT_LE_Set_Advertisement_Filter_Enable 命令后, 控制器应生成命令完成事件。

#### <a name="hci_vs_msft_read_absolute_rssi"></a>HCI_VS_MSFT_Read_Absolute_RSSI

HCI_VS_MSFT_Read_Absolute_RSSI 从控制器读取 BR/EDR 连接的**绝对**接收信号强度指示 (RSSI) 值。

|Command|代码|命令参数|返回参数|
|---|---|---|---|
|HCI_VS_MSFT_Read_Absolute_RSSI|选择的基本代码 |<ul><li>Subcommand_opcode</li><li>柄</li>|<ul><li>状态</li><li>Subcommand_opcode</li><li>柄</li><li>RSSI</li></ul>|

同时提供了一个连接句柄作为命令和返回参数来标识正在读取其 RSSI 的 ACL 连接。 RSSI 指标是绝对值到± 6 dB 准确性的**绝对**接收方信号强度。 如果无法读取 RSSI, 则 RSSI 度量值应设置为127。
控制器始终应始终使用命令完成事件立即完成此命令。

#### <a name="command_parameters"></a>Command_parameters

Subcommand_opcode (1 个八进制):

| ReplTest1  |  参数说明 |
|---|---|
|0x06|  HCI_VS_MSFT_Read_Absolute_RSSI 的子命令操作码。|

句柄 (2 个字节):

| ReplTest1  |  参数说明 |
|---|---|
|0x_XXXX_|必须读取其 RSSI 的 BR/EDR 连接的句柄。|

#### <a name="return_parameters"></a>Return_parameters

状态 (1 个八进制数):

|ReplTest1|参数说明|
|---|---|
|0x00|命令已成功。|
|0x01-0xFF|命令失败。 有关详细信息, 请参阅蓝牙核心规范中的_错误代码_。|

Subcommand_opcode (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x06|HCI_VS_MSFT_Read_Absolute_RSSI 的子命令操作码。|

句柄 (2 个字节):

|ReplTest1|参数说明|
|---|---|
|0xXXXX| 读取其 RSSI 的 BR/EDR 连接的句柄。|

RSSI (1 个八进制):

|     ReplTest1      |                                                  参数说明                                                   |
|----------------|--------------------------------------------------------------------------------------------------------------------------|
| N = RSSI 值 | BR/EDR 连接的 RSSI 值。<ul><li>范围:-128 &lt; =  N&lt;= 127 (带符号整数)</li><li>Unit: dBm</li> |

#### <a name="events_generated__unless_masked_away"></a>Events_generated__unless_masked_away

当 HCI_VS_MSFT_Read_Absolute_RSSI 命令完成时, 控制器应生成一个命令完成事件。

## <a name="microsoft-defined-bluetooth-hci-events"></a>Microsoft 定义的蓝牙 HCI 事件

所有 Microsoft 定义的蓝牙 HCI 事件均为供应商定义的事件, 并使用事件代码0xFF。 Microsoft 事件的事件数据始终以字符串的常量字符串开头, 以将 Microsoft 定义的事件与其他供应商定义的事件区分开来。 常量字符串的长度和值由控制器实施者定义, 并在响应[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)时返回。

|HCI 事件|描述|
|---|---|
|[HCI_VS_MSFT_Rssi_Event](#hci_vs_msft_rssi_event)|HCI_VS_MSFT_RSSI_Event 指示[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)命令已完成。|
|[HCI_VS_MSFT_LE_Monitor_Device_Event](#hci_vs_msft_le_monitor_device_event)|HCI_VS_MSFT_LE_Monitor_Device_Event 指示控制器已启动或停止监视蓝牙 LE 设备。|

### <a name="hci_vs_msft_rssi_event"></a>HCI_VS_MSFT_RSSI_Event

HCI_VS_MSFT_RSSI_Event 指示[HCI_VS_MSFT_Monitor_Rssi](#hci_vs_msft_monitor_rssi)命令已完成。
如果_Status_参数为零, 则该命令已完成, 因为远程设备的 RSSI 值更改为指定范围之外的值。 如果_Status_参数为非零, 则该命令已完成, 因为无法再监视连接的 RSSI 值。

|Event|事件代码|Microsoft 事件代码|事件参数|
|---|---|---|---|
|HCI_VS_MSFT_RSSI_Event|0xFF|0x01|<p>Event_prefix</p><p>Microsoft_event_code</p><p>状态</p><p>Connection_handle</p><p>RSSI</p>

#### <a name="event_parameters"></a>Event_parameters

Event_prefix (变量大小):

|ReplTest1|参数说明|
|---|---|
|事件前缀|将此事件标记为 Microsoft 定义的事件前缀。 大小和值与[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)命令返回的值相同。|

Microsoft_event_code (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x01|HCI_VS_MSFT_RSSI_Event 的事件代码。|

状态 (1 个八进制数):

|ReplTest1|参数说明|
|---|---|
|0x00|辉煌. 连接的 RSSI 值满足以下条件之一。<ul><li>RSSI 已达到或超过_RSSI_threshold_high_。</li><li>RSSI 在_RSSI_threshold_low_超过_RSSI_threshold_low_time_interval_秒。</li><li>_RSSI_sampling_period_已过期, 生成了此事件以通知主机 RSSI 值。</li></ul>|
|0x01&#160;-&#160;0xff|否则. 无法再监视连接的 RSSI 值。 错误代码通常是描述基础 ACL 连接丢失原因的代码之一。|

Connection_handle (2 个字节):

|ReplTest1|参数说明|
|---|---|
|0x_XXXX_|要监视其 RSSI 的连接的句柄。|

RSSI (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|N = _RSSI&#160;值_|用于连接的已测量链接 RSSI 值。 对于 BR/EDR:<ul><li>范围:-128 &lt; =  N&lt;= 127 (带符号整数)</li><li>Unit: dBm</li></ul>对于 LE:<ul><li>范围:-127 到 20 (带符号整数)</li><li>Unit: dBm</li></ul>|

### <a name="hci_vs_msft_le_monitor_device_event"></a>HCI_VS_MSFT_LE_Monitor_Device_Event

HCI_VS_MSFT_LE_Monitor_Device_Event 指示控制器已启动或停止监视蓝牙 LE 设备。

如果_Monitor_state_参数值为 1, 则控制器开始监视具有指定 BD_ADDR 的蓝牙设备。 如果_Monitor_state_参数值为 0, 则控制器停止监视具有指定 BD_ADDR 的蓝牙设备。

|Event|事件代码|Microsoft 事件代码|事件参数|
|---|---|---|---|
|HCI_VS_MSFT_LE_Monitor_Device_Event|0xFF|0x02|<p>Event_prefix</p><p>Microsoft_event_code</p><p>Address_type</p><p>BD_ADDR</p><p>Monitor_handle</p><p>Monitor_state</p>

如果尚未生成_Monitor_state_设置为1的 HCI_VS_MSFT_LE_Monitor_Device_Event, 控制器不应生成 HCI_VS_MSFT_LE_Monitor_Device_Event, 并将_Monitor_state_参数设置为0。

#### <a name="event_parameters"></a>Event_parameters

Event_prefix (变量大小):

|ReplTest1|参数说明|
|---|---|
|事件前缀|将此事件标记为 Microsoft 定义的事件前缀。 大小和值与[HCI_VS_MSFT_Read_Supported_Features](#hci_vs_msft_read_supported_features)命令返回的值相同。

Microsoft_event_code (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x02|HCI_VS_MSFT_LE_Monitor_Device_Event 的事件代码。|

Address_type (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x00|公用设备地址。|
|0x01|随机设备地址。|
|0x02&#160;-&#160;0xff|供将来使用的保留值。|

BD_ADDR (6 个字节):

|ReplTest1|参数说明|
|---|---|
|0x_XXXXXXXXXXXX_|设备的蓝牙地址。|

Monitor_handle (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x_XX_|为[HCI_VS_MSFT_LE_Monitor_Advertisement](#hci_vs_msft_le_monitor_advertisement)命令指定的筛选器的句柄。|

Monitor_state (1 个八进制):

|ReplTest1|参数说明|
|---|---|
|0x00|控制器停止监视由_BD_ADDR_和_Monitor_handle_指定的设备。|
|0x01|控制器已开始监视_BD_ADDR_和_Monitor_handle_指定的设备。|
