---
title: 蓝牙主机单选支持
ms.assetid: 7AA53797-F8DC-4FA6-9A19-E20289AF50CA
description: 提供有关 Windows 中的蓝牙主机单选支持问题和解答的列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03f6b403d7dd73869326dc0d9fa2b69e3934c66
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761856"
---
# <a name="bluetooth-host-radio-support"></a>蓝牙主机无线电支持

以下列表提供了 Bluetooth 无线电支持问与答：

- [在 Windows 中受支持的蓝牙主控制器](#bluetooth-host-controllers-supported-in-windows)
- [强制 Bluetooth 堆栈加载如果 Windows 不能匹配设备 ID (Windows Vista)](#forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-(windows-vista))
- [如何确保 Bluetooth 无线电收发器在 Windows Vista 中的内置支持](#how-to-ensure-in-box-support-for-bluetooth-radios-in-windows-vista)
- [第三方 INF 文件是否应使用了 Microsoft 定义的类 GUID](#whether-third-party-inf-files-should-use-the-microsoft-defined-class-guid)
- [为什么控件面板蓝牙应用程序在 Windows 7 中缺少](#why-the-control-panel-bluetooth-application-is-missing-in-windows-7)
- [为什么蓝牙图标不出现在任务栏中](#why-the-bluetooth-icon-does-not-appear-in-the-taskbar)
- [Windows 支持蓝牙单选固件更新](#windows-support-for-bluetooth-radio-firmware-updates)
- [Windows 支持的特定于供应商的传递命令](#windows-support-for-vendor-specific-pass-through-commands)
- [供应商提供的配置文件的 Windows 支持](#windows-support-for-vendor-supplied-profiles)
- [蓝牙配置文件和默认情况下启用的协议](#bluetooth-profiles-and-protocols-that-are-enabled-by-default)
- [组策略可以如何阻止蓝牙单选安装](#how-group-policy-can-block-bluetooth-radio-installation)
- [如何更改发布的 Windows 8 和 Windows 8.1 的设备 ID 配置文件记录](#how-to-change-the-device-id-profile-record-published-by-windows-8-and-windows-8.1)

## <a name="bluetooth-host-controllers-supported-in-windows"></a>在 Windows 中受支持的蓝牙主控制器

使用 Windows，蓝牙无线可打包为外部硬件保护装置或嵌入在一台计算机，但它必须连接到计算机的 USB 端口之一。 包含在 Windows 7 和 Windows Vista 的 Bluetooth 堆栈不支持蓝牙单选连接通过 PCI，I2C，串行、 安全数字 I/O (SDIO) CompactFlash，或 PC 卡接口。 在 Windows 8 和 Windows 8.1 中，可以通过第三方总线驱动程序添加备用传输方式通过连接的无线电收发器。 请参阅的可扩展的传输部分[蓝牙设备引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_bltooth/)有关详细信息。

## <a name="forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-windows-vista"></a>强制 Bluetooth 堆栈加载如果 Windows 不能匹配设备 ID (Windows Vista)

新的蓝牙无线可能不匹配任何设备中随 Windows 蓝牙 INF (Bth.inf) 的 Id。 这会阻止 Windows 加载设备的蓝牙堆栈。 Ihv 应确保其单选可使用本机 Bluetooth 堆栈中的以下方法之一：

- 创建引用 Bth.inf 单选 INF。 蓝牙无线的特定于供应商的 INF 文件的示例，请参阅[附录 b:在 Windows Vista 中使用的 INF 文件供应商提供的示例](bluetooth-faq--appendix-b.md)。
- 在指定适当的兼容和 subcompatible id。 设备固件中存储扩展的兼容 ID 操作系统描述符 有关的信息扩展兼容 ID 操作系统描述符，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=308932)。
- 强制加载的 Bluetooth 堆栈

以下过程概括介绍了如何使用设备管理器来强制加载新单选 Bluetooth 堆栈：

1. 运行控件面板设备管理器应用程序并识别蓝牙无线上的设备列表。
2. 若要运行更新驱动程序软件向导，右键单击 Bluetooth 无线电项，然后选择**更新驱动程序软件**。
3. 使用向导来强制安装蓝牙驱动。

此过程的详细说明，请参阅[附录 a:如何在 Windows Vista 中的新硬件上安装内置的蓝牙驱动程序](bluetooth-faq--appendix-a.md)。

## <a name="how-to-ensure-in-box-support-for-bluetooth-radios-in-windows-vista"></a>如何确保 Bluetooth 无线电收发器在 Windows Vista 中的内置支持

Ihv 应执行以下步骤，确保在 Windows 上其 Bluetooth 无线电收发器拥有在 box 支持部门：

- 请确保单选支持扩展的兼容 ID 操作系统功能描述符。 有关详细信息，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=617154)。
- 获得 Windows 认证计划批准 Bluetooth 无线电硬件和关联的 INF 文件。 蓝牙无线的特定于供应商的 INF 文件的示例，请参阅[附录 b:在 Windows Vista 中使用的 INF 文件供应商提供的示例](bluetooth-faq--appendix-b.md)。
- 使用合作伙伴中心可通过 Windows Update 提供的 INF 文件

不再可以现成 Bth.inf 文件适用于 Windows Vista 中添加的无线电收发器。

## <a name="whether-third-party-inf-files-should-use-the-microsoft-defined-class-guid"></a>第三方 INF 文件是否应使用了 Microsoft 定义的类 GUID

Ihv 应仅在引用中框蓝牙 INF 文件 (Bth.inf) 这些 INF 文件中的蓝牙设备使用 Microsoft 定义的类的全局唯一标识符 (GUID) ({e0cbf06c cd8b 4647 bb8a 263b43f0f974})。 这意味着设备使用的本机 Windows 共同安装程序、 服务和通知区域图标。 实现其自己的蓝牙驱动的 Ihv 必须创建特定于供应商类 GUID，并使用 WLK 测试工具来确保堆栈符合未分类的 Windows 认证计划。

## <a name="why-the-control-panel-bluetooth-application-is-missing-in-windows-7"></a>为什么控件面板蓝牙应用程序在 Windows 7 中缺少

在 Windows 7 中，控件面板蓝牙应用程序已合并到设备和打印机。 因此，调整 Bluetooth 无线电设置、 管理蓝牙设备，以及添加新蓝牙设备可以仅从设备和打印机中。

## <a name="why-the-bluetooth-icon-does-not-appear-in-the-taskbar"></a>为什么蓝牙图标不出现在任务栏中

如果蓝牙图标不出现在任务栏，则可能是由于一个或多个原因如下：

- 蓝牙无线功能处于关闭状态。
- 蓝牙无线处于仿真模式
- 在中**蓝牙设置**对话框中，**在通知区域中显示的蓝牙图标**未选中复选框

## <a name="windows-support-for-bluetooth-radio-firmware-updates"></a>Windows 支持蓝牙单选固件更新

目前，Windows 附带的蓝牙堆栈不直接支持固件更新。 但是，对于 Bluetooth 无线电收发器通过 USB 端口连接，Windows 支持符合 USB 设备固件更新 (DFU) 规范的固件更新。 通过 DFU 接口以执行固件更新并重新启动广播，Ihv 可以使用蓝牙无线创建进行通信的用户模式下实用程序。

## <a name="windows-support-for-vendor-specific-pass-through-commands"></a>Windows 支持的特定于供应商的传递命令

Windows 8.1、 Windows 8、 Windows 7 和 Windows Vista SP2 包括支持特定于供应商的传递命令。 这些内核模式接口记录在 WDK 中。

## <a name="windows-support-for-vendor-supplied-profiles"></a>供应商提供的配置文件的 Windows 支持

Windows 8.1、 Windows 8、 Windows 7 和 Windows Vista 支持供应商提供蓝牙配置文件。 但是，Windows XP 不支持。 在框 INF 文件 (Bth.inf) 中包含已由蓝牙 SIG 标准化这些配置文件的 Guid。

当用户与计算机蓝牙设备配对时，会将设备的配置文件与 Bth.inf 中列出的配置文件进行比较。 如果设备配置文件与这些配置文件之一不匹配，则用户将收到一个对话框，要求他们提供相应的供应商的软件。

想要特定于供应商的个人资料的供应商必须使用其自己的 GUID 和特定于供应商的 INF 文件中引用它。 此 INF 文件可以使用 Include 和需求指令以引用适当 Bth.inf 部分和指令。 有关特定于供应商的 INF 文件的示例，请参阅[附录 b:在 Windows Vista 中使用的 INF 文件供应商提供的示例](bluetooth-faq--appendix-b.md)。

## <a name="bluetooth-profiles-and-protocols-that-are-enabled-by-default"></a>蓝牙配置文件和默认情况下启用的协议

他是 Windows 附带的蓝牙驱动某些蓝牙配置文件的提供的内置支持。 供应商必须实现所需的服务以支持任何其他蓝牙配置文件，如最多为 USB 和 PCI。 Windows 可以使用默认情况下启用蓝牙配置文件，称为支持的配置文件-若要生成的物理设备对象 (PDOs)。 这样，需要启用该配置文件的驱动程序的默认加载。 可以通过查看下的 SupportedServices 和 UnsupportedServices 值标识注册表中支持的配置文件**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services\\Bthport\\参数**密钥。

> [!NOTE]
> 仅安装了 Bluetooth 的设备后，Bthport 密钥添加到注册表。

下表列出了 Windows 支持的 Bth.inf 中的配置文件。

|服务 ID|描述|
|----|----|
|{00001101-0000-1000-8000-00805f9b34fb}|SPP|
|{00001103-0000-1000-8000-00805f9b34fb}|DUN
|{00001124-0000-1000-8000-00805f9b34fb}|HID|
|{00001126-0000-1000-8000-00805f9b34fb}|HCRP|

### <a name="windows-xp-bluetooth-profiles"></a>Windows XP 蓝牙配置文件

下表列出了不受支持的蓝牙配置文件和协议。 请注意，在此上下文中，"不受支持"意味着 Windows 不会不会自动生成 PDO 或 devnode 或显示添加新的硬件向导。 因此，一些内置配置文件和协议处理，就好像它们是不受支持。 例如，SDP 是一种现成协议的蓝牙服务 id，但不需要 PDO。 SDP 协议因此标记为 Bth.inf 中不受支持，以避免在 PDO 创建

|服务 ID|在框|描述|
|----|----|----|
|{0000110a-0000-1000-8000-00805f9b34fb}|否|音频源|
|{0000110c-0000-1000-8000-00805f9b34fb}|否|AV 远程目标|
|{00001001-0000-1000-8000-00805f9b34fb}|否|浏览组服务|
|{00001111-0000-1000-8000-00805f9b34fb}|否|传真服务|
|{0000111f-0000-1000-8000-00805f9b34fb}|否|Handsfree 音频网关|
|{00001112-0000-1000-8000-00805f9b34fb}|否|耳机音频网关|
|{00001104-0000-1000-8000-00805f9b34fb}|否|红外移动通信 (IRMC) 同步服务|
|{00001107-0000-1000-8000-00805f9b34fb}|否|IRMC 同步命令|
|{00001106-0000-1000-8000-00805f9b34fb}|是|Obex 文件传输|
|{00001105-0000-1000-8000-00805f9b34fb}|是|对象推送|
|{00001117-0000-1000-8000-00805f9b34fb}|否|平移组临时网络 (GN)|
|{00001116-0000-1000-8000-00805f9b34fb}|否|平移网络接入点 (NAP)|
|{00001115-0000-1000-8000-00805f9b34fb}|是|平移 U|
|{0000112e-0000-1000-8000-00805f9b34fb}|否|电话薄客户端设备 (PCE) 服务|
|{0000112f-0000-1000-8000-00805f9b34fb}|否|通讯簿服务器设备 (PSE) 服务|
|{00001200-0000-1000-8000-00805f9b34fb}|是|即插即用服务|
|{00001002-0000-1000-8000-00805f9b34fb}|否|公共浏览组服务|
|{00001000-0000-1000-8000-00805f9b34fb}|是|SDP|
|{0000112d-0000-1000-8000-00805f9b34fb}|否|Sim 访问|

如果 Ihv 不希望 Windows 自动生成一个为其设备的 PDO，他们可以将服务 GUID 添加到不受支持的服务列表。 有关示例，请参阅 Bth.inf。

## <a name="how-group-policy-can-block-bluetooth-radio-installation"></a>组策略可以如何阻止蓝牙单选安装

有关如何使用组策略来阻止安装 Bluetooth 无线电收发器的详细信息，请参阅的"禁止安装被禁止设备的"一节[控制设备安装和使用组策略的使用情况的循序渐进指南](https://go.microsoft.com/fwlink/p/?linkid=324335).

使用蓝牙无线以下兼容 Id:

USB\\类\_（对于基于 USB 的无线电收发器） E0 MS\_BTHX\_BTHMINI （适用于非 USB 无线收发器）

> [!NOTE]
> 如果已安装，这不会删除蓝牙驱动程序支持。 此外，此策略需要将应用到预安装映像。

## <a name="how-to-change-the-device-id-profile-record-published-by-windows-8-and-windows-81"></a>如何更改发布的 Windows 8 和 Windows 8.1 的设备 ID 配置文件记录

设备 ID 配置文件定义可用于提供到远程设备的标识信息的 SDP 记录。 以前和当前 Windows 版本具有用于发布到配对的设备上的设备 ID 记录为泛型蓝牙服务提供特定于设备的硬件 Id。

从 Windows 8 开始，Windows 还会发布本地的设备 ID 记录到远程的蓝牙设备 Windows 8 设备进行标识。 Oem 可以更好地识别其特定的 Windows 8 设备可调整的默认值。 这些值定义如 HKLM 下的以下表中所示\\系统\\CCS\\services\\BTHPORT\\Parameters 注册表项：

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
<th align="left"><p>在任务栏的搜索框中键入</p></th>
<th align="left"><p>描述</p></th>
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
<td align="left"><p>OEM 指定 VendorID</p></td>
<td align="left"><p>0x06-Microsoft 供应商 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>DIDProductID</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定 ProductID</p></td>
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
