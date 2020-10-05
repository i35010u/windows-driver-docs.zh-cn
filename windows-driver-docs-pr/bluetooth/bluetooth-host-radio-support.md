---
title: 蓝牙主机无线电支持
ms.assetid: 7AA53797-F8DC-4FA6-9A19-E20289AF50CA
description: 提供有关 Windows 中的蓝牙主机无线电支持的问题和解答列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 648404b2c0c39e3e370b2c7b2edd752b36affc38
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733441"
---
# <a name="bluetooth-host-radio-support"></a>蓝牙主机无线电支持

本主题提供有关蓝牙无线电支持的常见问题解答。

## <a name="bluetooth-host-controllers-supported-in-windows"></a>Windows 中支持的蓝牙主机控制器

使用 Windows，可以将蓝牙无线电打包为外部转换器或嵌入在计算机内，但必须连接到计算机的 USB 端口之一。 Windows 7 和 Windows Vista 附带的蓝牙堆栈不支持通过 PCI、I2C、串行、安全数字 i/o (SDIO) 、CompactFlash 或 PC 卡接口进行蓝牙无线电连接。 在 Windows 8 和 Windows 8.1 中，可以通过第三方总线驱动程序添加通过备用传输连接的收音机。 有关详细信息，请参阅 [蓝牙设备参考](/windows-hardware/drivers/ddi/_bltooth/) 的可扩展传输部分。

## <a name="forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-windows-vista"></a>如果 Windows 无法与 Windows Vista (的设备 ID 匹配，则强制加载蓝牙堆栈) 

新的蓝牙无线电可能与 Windows 附带 (Bth) 中的任何设备 Id 都不匹配。 这会阻止 Windows 加载设备的蓝牙堆栈。 Ihv 应通过以下方式之一确保其无线电适用于本机蓝牙堆栈：

* 为引用 Bth 的收音机创建 INF。 有关蓝牙收音机的供应商特定 INF 文件的示例，请参阅 [附录 B：供应商提供的用于 Windows Vista 的 Inf 文件的示例](bluetooth-faq--appendix-b.md)。
* 在设备固件中存储扩展的兼容 ID 操作系统描述符，以指定相应的兼容和 subcompatible ID。 有关扩展兼容 ID 操作系统描述符的信息，请参阅 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10))。
* 强制加载蓝牙堆栈

以下过程使用设备管理器强制为新的收音机加载蓝牙堆栈：

1. 运行控制面板设备管理器应用程序，并在设备列表上标识蓝牙收音机。
2. 若要运行更新驱动程序软件向导，请右键单击蓝牙单选项目，然后选择 " **更新驱动程序软件**"。
3. 使用向导强制安装蓝牙堆栈。

有关此过程的详细说明，请参阅 [附录 a：如何在 Windows Vista 中的新硬件上安装内置的蓝牙驱动程序](bluetooth-faq--appendix-a.md)。

## <a name="ensure-in-box-support-for-bluetooth-radios"></a>确保对蓝牙无线电收发器提供内置支持

Ihv 应采取以下步骤来确保其蓝牙无线电支持 Windows 上的 box：

* 确保该无线电支持扩展的兼容 ID OS 功能描述符。 有关详细信息，请参阅 [MICROSOFT OS 描述符](../usbcon/microsoft-os-1-0-descriptors-specification.md)。
* 获取针对蓝牙无线电硬件和关联 INF 文件的 Windows 认证计划批准。 有关蓝牙收音机的供应商特定 INF 文件的示例，请参阅 [附录 B：供应商提供的用于 Windows Vista 的 Inf 文件的示例](bluetooth-faq--appendix-b.md)。
* 使用 "合作伙伴中心" 使 INF 文件可通过 Windows 更新

不能再将无线收发器添加到内置的 Bth 文件中。

## <a name="should-third-party-inf-files-use-the-microsoft-defined-class-guid"></a>第三方 INF 文件是否应使用 Microsoft 定义的类 GUID

Ihv 应使用 Microsoft 定义的类全局唯一标识符 (GUID) 仅适用于那些引用内置 Bluetooth INF 文件 (Bth) 的 INF 文件中的蓝牙设备 ( {e0cbf06c cd8b 4647 bb8a 263b43f0f974 ) }。 这意味着设备使用本机 Windows co 安装程序、服务和通知区域图标。 实现其自己的蓝牙堆栈的 Ihv 必须创建特定于供应商的类 GUID，并使用 WLK 测试工具确保堆栈符合未分类的 Windows 认证计划。

## <a name="why-the-control-panel-bluetooth-application-is-missing"></a>为什么缺少 "控制面板" 蓝牙应用程序

控制面板蓝牙应用程序已合并到设备和打印机中。 因此，只可以在设备和打印机中调整蓝牙无线电设置，管理 Bluetooth 设备并添加新的蓝牙设备。

## <a name="why-the-bluetooth-icon-might-not-appear-in-the-taskbar"></a>为什么 "蓝牙" 图标可能不会出现在任务栏中

如果任务栏中没有蓝牙图标，可能是由于以下一个或多个原因：

* 蓝牙无线功能处于关闭状态。
* 蓝牙无线电处于仿真模式。
* 在 " **蓝牙设置** " 对话框中，未选择 "在 **通知区域中显示蓝牙图标** " 复选框。

## <a name="windows-support-for-bluetooth-radio-firmware-updates"></a>Windows 对蓝牙收音机固件更新的支持

目前，Windows 附带的蓝牙堆栈不直接支持固件更新。 但是，对于通过 USB 端口连接的蓝牙无线电收发器，Windows 支持固件更新，与 USB 设备固件更新 (DFU) 规范兼容。 Ihv 可以通过 DFU 接口创建与蓝牙收音机通信的用户模式实用工具，以执行固件更新并重新启动无线电。

## <a name="windows-support-for-vendor-specific-pass-through-commands"></a>Windows 对特定于供应商的传递命令的支持

Windows 包括对特定于供应商的传递命令的支持。 WDK 中介绍了这些内核模式接口。

## <a name="windows-support-for-vendor-supplied-profiles"></a>Windows 对供应商提供的配置文件的支持

Windows 支持供应商提供的蓝牙配置文件。 已由蓝牙 SIG 标准化的配置文件的 Guid 包括在 (Bth ") 中的" in "INF 文件中。

当用户将蓝牙设备与计算机配对时，会将设备的配置文件与 Bth 中列出的配置文件进行比较。 如果设备配置文件与其中一个配置文件不匹配，则用户会收到一个对话框，询问他们是否提供相应的供应商软件。

需要供应商特定配置文件的供应商必须使用其自己的 GUID，并在特定于供应商的 INF 文件中引用它。 此 INF 文件可使用 Include 和 use 指令引用适当的 Bth 节和指令。 有关供应商特定 INF 文件的示例，请参阅 [附录 B：供应商提供的用于 Windows Vista 的 Inf 文件的示例](bluetooth-faq--appendix-b.md)。

## <a name="bluetooth-profiles-and-protocols-that-are-enabled-by-default"></a>默认情况下启用的蓝牙配置文件和协议

Windows 附带的蓝牙堆栈只为某些蓝牙配置文件提供内置支持。 供应商必须实现所需的服务来支持任何其他蓝牙配置文件，这一点与用于 USB 和 PCI 的操作非常相似。 Windows 可以使用默认情况下启用的蓝牙配置文件（称为受支持的配置文件）来生成 (PDOs) 的物理设备对象。 这会启用启用配置文件所需的驱动程序的默认加载。 您可以通过查看 " **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services \\ Bthport \\ 参数** " 项下的 SupportedServices 和 UnsupportedServices 值来标识注册表中支持的配置文件。

> [!NOTE]
> 只有在安装了 Bluetooth 设备后，Bthport 密钥才会添加到注册表中。

下表列出了 Windows 支持的 Bth 中的配置文件。

|服务 ID|说明|
|----|----|
|{00001101-0000-1000-8000-00805f9b34fb}|SPP|
|{00001103-0000-1000-8000-00805f9b34fb}|DUN
|{00001124-0000-1000-8000-00805f9b34fb}|HID|
|{00001126-0000-1000-8000-00805f9b34fb}|HCRP|

### <a name="windows-bluetooth-profiles"></a>Windows 蓝牙配置文件

若要使启用 Bluetooth 的设备或附件适用于运行 Windows 10 的电脑，设备需要使用其中一个受支持的蓝牙配置文件。 请参阅 [支持的蓝牙配置文件](https://support.microsoft.com/help/10568/windows-10-supported-bluetooth-profiles)中的最新列表。

如果 Ihv 不希望 Windows 为其设备自动生成 PDO，则可以将服务 GUID 添加到不受支持的服务列表中。 有关示例，请参阅 Bth。

## <a name="how-group-policy-can-block-bluetooth-radio-installation"></a>组策略如何阻止蓝牙无线安装

有关如何使用组策略阻止安装蓝牙无线电收发器的详细信息，请参阅 [使用组策略控制设备安装和使用](/previous-versions/dotnet/articles/bb530324(v=msdn.10))的循序渐进指南中的 "阻止安装禁止的设备" 部分。

为蓝牙无线电使用以下兼容 Id：

USB \\ 类 \_ E0 (适用于基于 USB 的无线电) MS \_ BTHX \_ BTHMINI (，适用于非 usb 收音机) 

> [!NOTE]
> 如果蓝牙驱动程序已安装，则不会删除该支持。 此外，需要将此策略应用到预安装映像。

## <a name="how-to-change-the-device-id-profile-record-published-by-windows"></a>如何更改 Windows 发布的设备 ID 配置文件记录

设备 ID 配置文件定义可用于向远程设备提供标识信息的 SDP 记录。 以前的 Windows 版本和当前版本使用成对设备上发布的设备 ID 记录为通用蓝牙服务提供特定于设备的硬件 Id。

Windows 还发布了一个本地设备 ID 记录，用于识别远程蓝牙设备的 Windows 设备。 Oem 可以调整默认值，以便更好地识别其特定的 Windows 设备。 这些值定义如下表中的 HKLM \\ System \\ CCS \\ services \\ BTHPORT \\ Parameters 注册表项：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="odd">
<th align="left"><p>ValueName</p></th>
<th align="left"><p>类型</p></th>
<th align="left"><p>说明</p></th>
<th align="left"><p>默认值</p></th>
</tr>
</thead>
<tbody>
<tr class="even">
<td align="left"><p>DIDVendorIDSource</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>0x01 = 蓝牙 SIG 命名空间</p>
<p>0x02 = USB 论坛命名空间</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DIDVendorID</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定的 VendorID</p></td>
<td align="left"><p>0x06 – Microsoft 供应商 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>DIDProductID</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定的 ProductID</p></td>
<td align="left"><p>0x01 – Microsoft Windows</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DIDVersion</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定的产品版本</p></td>
<td align="left"><p>0x0800 – Windows 8</p></td>
</tr>
</tbody>
</table>