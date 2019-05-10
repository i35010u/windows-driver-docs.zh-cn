---
Description: 想要构建通过 USB 类型 C 连接器的 Windows 系统的 Oem 的常见问题。
title: 常见问题-Windows 系统上的 USB C 型连接器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 348dbf3f3cb81c05fea4ae6421de1b7d575d86b8
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405051"
---
# <a name="faq-usb-type-c-connector-on-a-windows-system"></a>常见问题解答：Windows 系统上的 USB 类型 C 连接器

**上次更新时间**-2016 年 12 月

**Windows 版本**:

* Windows 10 桌面版（家庭版、专业版、企业版和教育版）
* Windows 10 移动版

想要构建通过 USB 类型 C 连接器的 Windows 系统的 Oem 的常见问题。

* [USB 类型 C 连接器功能](#usb-type-c-connector-features)
* [备用模式需要进行协商，如分发点 2 道 vs 操作系统输入。DP 4-lane](#operating-system-input-into-which-alternate-mode-needs-to-be-negotiated-such-as-dp-2-lane-vs-dp-4-lane)
* [预操作系统与类型 C PD 收费](#pre-os-charging-with-type-c-and-pd)
* [若要启用扩展方案，如连续体的 USB 主机时收费电话](#charging-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum)
* [Windows 10 移动版支持 USB 布告栏设备](#windows-10-mobile-support-of-usb-billboard-devices)
* [在早期版本的 Windows 上支持 USB 类型-C](#support-for-usb-type-c-on-earlier-versions-of-windows)
* [在早期版本的 Windows 支持 UCSI](#ucsi-support-on-earlier-versions-of-windows)
* [如何测试 UCSI 的实现](#how-to-test-an-implementation-of-ucsi)
* [条件和不同的错误的用户界面](#conditions-and-ui-for-the-different-errors)
* [非 PD 端口连接到 PD 提供程序并不是 PD 提供程序的系统的 PD 使用者](#connecting-a-non-pd-port-to-a-pd-provider-and-a-pd-consumer-to-a-system-that-is-not-a-pd-provider)
* [连接到不支持这些功能的 PC 的闪电、 SuperMHL 或 PCI express](#connecting-thunderbolt-supermhl-or-pci-express-to-a-pc-that-does-not-support-those-capabilities)
* [支持和 MTP 通过 USB 类型-C 在 Windows 中的限制](#support-and-limitations-for-mtp-over-usb-type-c-in-windows)
* [如何向下游设备和中心建立连接和通信与 USB 连接器管理器 (UCM)](#how-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm-)
* [USB 类型 C MUTT HLK 测试要求](#usb-type-c-mutt-requirements-for-hlk-tests)
* [Microsoft 支持 P2P 之间的数据传输相同的 Windows 10 SKU](#microsoft-support-for-P2P-data-transfer-between-the-same-windows-10-sku)
* [UCM 类扩展 (UcmCx) 通信使用 PMIC 或电池驱动程序来获取或设置充电状态](#ucm-class-extension-ucmcx-communication-with-pmic-or-battery-driver-to-getset-charging-status)
* [HLK 支持 USB 类型-C](#hlk-support-for-usb-type-c)
* [UCSI](#ucsi)
* [测试 Windows 10 上运行的 UCSI 实现](#test-a-ucsi-implementation-running-on-windows-10)
* [测试 Windows 10 上的 UCMCx 客户端驱动程序](#test-a-ucmcx-client-driver-on-windows-10)
* [VBus/VConn 控制和角色切换由 UCM 类扩展插件处理的操作](#vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension)

## <a name="usb-type-c-connector-features"></a>USB 类型 C 连接器功能

### <a name="symmetric-and-reversible-design"></a>对称和可逆设计

* 连接器已*对称*。 电缆有 USB 类型 C 连接器上允许使用 USB 类型 C 连接器对主机和函数设备每一端。 下面是将连接器进行比较的图像：
* 连接器旨在作为*可逆*。 传统的连接器必须已连接"右端的启动"。 使用可逆的设计中，可以翻转连接器。

### <a name="supports-all-usb-device-speeds"></a>支持所有 USB 设备的速度

连接器可支持 SuperSpeed （包括 SS +） 是低速度、 最快速度、 高速的 USB 设备。

### <a name="alternate-modes"></a>备用模式

连接器可以支持*备用模式*。 备用模式功能允许非 USB 协议通过 USB 电缆，运行时同时保留 USB 2.0 和计费功能。 目前，最受欢迎的备用模式是 DisplayPort/DockPort 和 MHL。

* **DisplayPort** /**DockPort**

  此备用模式允许用户通过 USB 连接器投影到外部 DisplayPort 显示音频/视频。

* **MHL**

  MHL 备用模式是允许对项目视频/音频向外部用户显示支持 MHL。

* **宣传位置错误消息**

  如果用户连接的 USB 类型 C 备用模式设备或附加的电脑或手机不支持的适配器时，设备或适配器可以公开布告栏设备，其中包含有关错误条件，以帮助用户解决问题的信息。

* **更高的能力限制**

   使用 USB 类型 C 连接器的系统具有更高版本的 power 限制，它可以支持多达 5V、 3A，15W。

   此外，可以选择性地支持连接器*电源交付*功能由定义[USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)OEM。 如果连接器支持 power 交付，USB C 类型系统可电源源提供程序或使用者，且支持多达 100W。

* **支持 USB 双角色**

  外围设备可以连接到移动与 USB 类型 C 连接器，将移动系统的传统角色从函数更改为主机系统。 当同一个系统连接到 PC 时，系统恢复函数的角色，并且 PC 将成为主机。

## <a name="operating-system-input-into-which-alternate-mode-needs-to-be-negotiated-such-as-dp-2-lane-vs-dp-4-lane"></a>备用模式需要进行协商，如分发点 2 道 vs 操作系统输入。DP 4 球道

否。 操作系统 （或任何由 Microsoft 提供的软件组件） 不起任何作用中选择备用模式。 通过连接器，特别是 USB 连接器管理器 (UCM) 客户端驱动程序的驱动程序做出的决定。 该驱动程序，会使用硬件接口，使用连接器的固件进行通讯。

## <a name="pre-os-charging-with-type-c-and-pd"></a>预操作系统与类型 C PD 收费

启用预操作系统充电属于由 OEM。 您可以选择不实现[USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)，并在 USB 类型 C power 级别，直到您启动到操作系统的费用。

## <a name="charging-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum"></a>若要启用扩展方案，如连续体的 USB 主机时收费电话

下面是需要考虑的一些事项：

* 必须实现[USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)，以便可以独立地交换功能和数据的角色。
* 停靠的上游端口应作为充电 UFP，USB 类型 C 规范中定义。 有关详细信息，请参阅部分 4.8.4，版本 1.1。
* 在停靠应请求在灾难恢复\_交换如果它解析为 DFP 或 PR\_如果它解析为 UFP 交换。

  初始 DFP 是电源，因此必须更改数据角色。 初始 UFP 是 power 接收器中，因此必须更改 power 角色。 您可以在实现这些回调函数中执行这些操作：

## <a name="windows10-mobile-support-of-usb-billboard-devices"></a>Windows 10 移动版支持 USB 布告栏设备

是的如果将该手机连接到支持 USB 布告栏，为每个设备[布告栏设备规范的 USB 设备类定义](https://go.microsoft.com/fwlink/p/?linkid=620207)，通知用户。 USB 连接器管理器 (UCM) 客户端驱动程序不需要处理通知。 如果您的系统无法识别备用模式下，不要输入模式。

## <a name="support-for-usb-type-c-on-earlier-versions-of-windows"></a>在早期版本的 Windows 上支持 USB 类型-C

USB C 类型不支持在 Windows 10 之前的 Windows 版本上。

## <a name="ucsi-support-on-earlier-versions-of-windows"></a>在早期版本的 Windows 支持 UCSI

UCSI 不支持在 Windows 10 之前的 Windows 版本上。

## <a name="how-to-test-an-implementation-of-ucsi"></a>如何测试 UCSI 的实现

若要测试您的实现，请遵循中给出的准则[USB 类型 C 手动互操作性测试过程](type.md)。 我们建议运行 USB 测试适用于 Windows 10 的 Windows 硬件 Lab Kit (HLK) 中。 这些测试所示[USB 的 Windows 硬件认证工具包测试](windows-hardware-certification-kit-tests-for-usb.md)。

## <a name="conditions-and-ui-for-the-different-errors"></a>条件和不同的错误的用户界面

Windows 10 可以显示一系列 USB 类型 C 错误消息，可帮助使用户了解使用 USB 类型 C 硬件和软件的不同组合的限制。 例如，用户可能会收到"设备正在充电缓慢"消息如果充电器连接到 USB 类型 C 连接器功能强大，足以，请与系统不兼容或已连接到非充电的端口。 有关详细信息，请参阅[USB 类型 C Windows 系统的消息疑难解答](https://go.microsoft.com/fwlink/?LinkId=526894)。

## <a name="connecting-a-non-pd-port-to-a-pd-provider-and-a-pd-consumer-to-a-system-that-is-not-a-pd-provider"></a>非 PD 端口连接到 PD 提供程序并不是 PD 提供程序的系统的 PD 使用者

非 PD 端口尝试通过使用 USB 类型 C 当前级别收费系统。 有关详细信息，请参阅[USB 3.1 和 USB 类型 C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)。

## <a name="connecting-thunderbolt-supermhl-or-pci-express-to-a-pc-that-does-not-support-those-capabilities"></a>连接到不支持这些功能的 PC 的闪电、 SuperMHL 或 PCI express

备用模式功能允许非 USB 协议 （如闪电，SuperMHL） 通过 USB 电缆，运行时同时保留 USB 2.0 和计费功能。 如果用户连接的 USB 类型 C 备用模式设备或附加电脑或手机运行 Windows 10 不支持的适配器时，检测到错误条件，并向用户显示一条消息。

* 如果设备或适配器公开布告栏设备，用户会看到有关错误条件，以帮助进行故障排除问题的信息。 Windows 10 的宣传位置设备提供现成驱动程序，并通知用户，出现错误。
* 用户可能会看到如下错误通知，"尝试改进 USB 连接"。 有关详细信息，请参阅[USB 类型 C Windows 系统的错误消息](introduction-to-usb-type-c-connectors.md#-4)。

为获得最佳结果，请确保通过 PC 或电话或电缆满足备用模式设备或适配器的要求。

## <a name="support-and-limitations-for-mtp-over-usb-type-c-in-windows"></a>支持和 MTP 通过 USB 类型-C 在 Windows 中的限制

面向桌面版本的 Windows 10 支持 MTP 中发起方角色中;Windows 10 移动版支持 MTP 响应方角色中。

## <a name="how-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm"></a>如何向下游设备和中心建立连接和通信与 USB 连接器管理器 (UCM)

UCM 是其自己的设备堆栈 (请参阅[体系结构：Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md))。 Windows 10 支持 USB 类型-C 包括所需的探测功能，以便确保不同的类驱动程序知道如何与不同的 USB 类型 C 连接器进行通信。 若要获取 Windows 10 支持 USB 类型-C，必须插入 UCM 设备堆栈。

## <a name="usb-type-c-mutt-requirements-for-hlk-tests"></a>USB 类型 C MUTT HLK 测试要求

Windows HLK 适用于 Windows 10 的包含 USB 主机和函数控制器的测试。 若要测试您的系统，请使用 USB C 一个适配器。 这些测试所示[USB 的 Windows 硬件认证工具包测试](windows-hardware-certification-kit-tests-for-usb.md)。

## <a name="microsoft-support-for-p2p-data-transfer-between-the-same-windows10-sku"></a>Microsoft 支持 P2P 之间的数据传输相同的 Windows 10 SKU

这不是有效的连接。

* 无法连接两台运行 Windows 10 桌面版的 Pc。
* 无法连接两个运行 Windows 10 移动版的移动设备。

如果用户尝试进行此类连接，Windows 将显示一条错误消息。 有关详细信息，请参阅[USB 类型 C Windows 系统的错误消息](introduction-to-usb-type-c-connectors.md#-6)。

Windows 移动设备和 Windows 桌面设备之间是唯一有效的连接。

## <a name="ucm-class-extension-ucmcx-communication-with-pmic-or-battery-driver-to-getset-charging-status"></a>UCM 类扩展 (UcmCx) 通信使用 PMIC 或电池驱动程序来获取或设置充电状态

在软件辅助充电平台，UcmCx 与 PMIC 和电池子系统进行通信。 客户端驱动程序可能会通过与通过硬件接口硬件通信确定计费级别。 硬件辅助的平台上嵌入式的控制器负责进行收费。 在过程中不涉及 UcmCx。

## <a name="hlk-support-for-usb-type-c"></a>HLK 支持 USB 类型-C

在 Windows HLK 适用于 Windows 10 中没有 USB 类型 C 的特定测试。 我们建议在 Windows HLK 适用于 Windows 10 中运行 USB 测试。 这些测试所示[USB 的 Windows 硬件认证工具包测试](windows-hardware-certification-kit-tests-for-usb.md)。

## <a name="ucsi"></a>UCSI

USB 类型 C 连接器系统软件接口 (UCSI) 规范介绍 USB 类型 C 连接器系统软件接口 (UCSI) 的功能并介绍了的硬件组件设计器，系统构建者寄存器和数据结构和设备驱动程序开发人员。 获取从规范[此站点](https://go.microsoft.com/fwlink/p/?LinkId=703713)。

Microsoft 提供了与 Windows，UcmUcsi.sys，实现功能规范所定义的现成驱动程序。 此驱动程序适用于具有嵌入式控制器的系统。

## <a name="test-a-ucsi-implementation-running-on-windows10"></a>测试 Windows 10 上运行的 UCSI 实现

我们建议在 Windows HLK 适用于 Windows 10 中运行 USB 测试。 这些测试所示[USB 的 Windows 硬件认证工具包测试](windows-hardware-certification-kit-tests-for-usb.md)。

## <a name="test-a-ucmcx-client-driver-on-windows10"></a>测试 Windows 10 上的 UCMCx 客户端驱动程序

我们建议在 Windows HLK 适用于 Windows 10 中运行 USB 测试。 这些测试所示[USB 的 Windows 硬件认证工具包测试](windows-hardware-certification-kit-tests-for-usb.md)。

## <a name="vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension"></a>VBus/VConn 控制和角色切换由 UCM 类扩展插件处理的操作

UCM 类扩展可能会从操作系统更改的连接器的数据或电源方向 get 请求。 在收到这些请求，它将调用的客户端驱动程序实现[ *EVT\_UCM\_连接器\_设置\_数据\_角色*](https://msdn.microsoft.com/library/windows/hardware/mt187818)并[ *EVT\_UCM\_连接器\_设置\_POWER\_角色*](https://msdn.microsoft.com/library/windows/hardware/mt187819)回调函数 (如果连接器实现 PD）。 在实现中，客户端驱动程序是预期的控制 VBUS 和 VCONN pin。 有关这些回调函数的详细信息，请参阅[写入 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)。
