---
description: 希望用 USB 类型 C 连接器构建 Windows 系统的 Oem 的常见问题。
title: FAQ-Windows 系统上的 USB 类型 C 连接器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f33263e88f3901518a2dfeeb4ee83c527bf472
ms.sourcegitcommit: b75e9940d49410e2b952e96f325df67a039cd571
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92336932"
---
# <a name="faq-usb-type-c-connector-on-a-windows-system"></a>常见问题解答：Windows 系统上的 USB 类型 C 连接器

## <a name="windows-versions"></a>Windows 版本

- Windows 10 桌面版（家庭版、专业版、企业版和教育版）
- Windows 10 移动版

针对想要用 USB 类型 C 连接器构建 Windows 系统的 Oem 的常见讨论点。

- [USB 类型 C 连接器功能](#usb-type-c-connector-features)
- [需要协商备用模式的操作系统输入，例如 DP 2 通道与 DP 4 通道](#operating-system-input-into-which-alternate-mode-needs-to-be-negotiated-such-as-dp-2-lane-vs-dp-4-lane)
- [类型 C 和 PD 的预操作系统收费](#pre-os-charging-with-type-c-and-pd)
- [在电话为 USB 主机时对电话进行收费，以启用扩展方案，例如 Continuum](#charging-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum)
- [USB 布告栏设备的 Windows 10 移动版支持](#windows10-mobile-support-of-usb-billboard-devices)
- [在早期版本的 Windows 上支持 USB 类型 C](#support-for-usb-type-c-on-earlier-versions-of-windows)
- [Windows 早期版本上的 UCSI 支持](#ucsi-support-on-earlier-versions-of-windows)
- [如何测试 UCSI 的实现](#how-to-test-an-implementation-of-ucsi)
- [不同错误的条件和 UI](#conditions-and-ui-for-the-different-errors)
- [将非 PD 端口连接到 PD 提供程序，将 PD 使用者连接到不是 PD 提供程序的系统](#connecting-a-non-pd-port-to-a-pd-provider-and-a-pd-consumer-to-a-system-that-is-not-a-pd-provider)
- [将闪电、SuperMHL 或 PCI express 连接到不支持这些功能的电脑](#connecting-thunderbolt-supermhl-or-pci-express-to-a-pc-that-does-not-support-those-capabilities)
- [Windows 中通过 USB 类型 C 进行 MTP 的支持和限制](#support-and-limitations-for-mtp-over-usb-type-c-in-windows)
- [下游设备和集线器如何连接并与 USB 连接器管理器通信 (UCM) ](#how-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm)
- [针对 HLK 测试的 USB 类型-C MUTT 要求](#usb-type-c-mutt-requirements-for-hlk-tests)
- [Microsoft 对同一 Windows 10 SKU 之间的 P2P 数据传输的支持](#microsoft-support-for-p2p-data-transfer-between-the-same-windows10-sku)
- [UCM class extension (UcmCx) 与 PMIC 或电池驱动程序通信，以获取/设置充电状态](#ucm-class-extension-ucmcx-communication-with-pmic-or-battery-driver-to-getset-charging-status)
- [对 USB 类型 C 的 HLK 支持](#hlk-support-for-usb-type-c)
- [UCSI](#ucsi)
- [测试 Windows 10 上运行的 UCSI 实现](#test-a-ucsi-implementation-running-on-windows-10)
- [在 Windows 10 上测试 UCMCx 客户端驱动程序](#test-a-ucmcx-client-driver-on-windows-10)
- [UCM 类扩展处理的 VBus/VConn 控件和角色切换操作](#vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension)

## <a name="usb-type-c-connector-features"></a>USB 类型 C 连接器功能

### <a name="symmetric-and-reversible-design"></a>对称和可逆设计

- 连接器为 *对称*连接器。 每个端点上都有一个 USB 类型 C 连接器，允许主机和功能设备使用 USB 类型 C 连接器。 下面是比较连接器的图像：
- 连接器设计为 *可逆*。 传统连接器必须连接到 "右对齐"。 利用可逆的设计，可以翻转连接器。

### <a name="supports-all-usb-device-speeds"></a>支持所有 USB 设备速度

连接器可以支持速度快、全速、高速、SuperSpeed (包括 SS +) 的 USB 设备。

### <a name="alternate-modes"></a>备用模式

连接器可以支持 *备用模式*。 备用模式功能允许非 USB 协议通过 USB 电缆运行，同时保留 USB 2.0 和充电功能。 目前，最常用的备用模式为 DisplayPort/DockPort 和 MHL。

#### <a name="displayport--dockport"></a>DisplayPort / DockPort

  此备用模式允许用户将音频/视频投影到外部 DisplayPort 通过 USB 连接器显示。

#### <a name="mhl"></a>MHL

  MHL 备用模式允许用户将视频/音频投影到支持 MHL 的外部显示器。

### <a name="billboard-error-messages"></a>布告栏错误消息

  如果用户连接的 USB 类型为 C 的备用模式设备或适配器不受连接的 PC 或手机支持，则设备或适配器可以公开一个布告栏设备，其中包含有关错误条件的信息，以帮助用户解决问题。

## <a name="increased-power-limits"></a>增加的电源限制

   使用 USB 类型 C 连接器的系统具有更高的电源限制，最多可支持5V、3A、15W。

   此外，连接器可以选择支持[USB 电源交付](https://www.usb.org/usb-charger-pd)OEM 定义的*电源交付*功能。 如果连接器支持电源交付，则 USB 类型 C 系统可以是电源提供商，也可以是使用者，支持最多100W。

## <a name="supports-usb-dual-roles"></a>支持 USB 双重角色

  外围设备可以使用 USB 类型 C 连接器连接到移动系统，从而将移动系统的传统角色从功能更改为主机。 当同一个系统连接到 PC 时，系统将恢复某个功能的角色，而 PC 会成为该主机。

## <a name="operating-system-input-into-which-alternate-mode-needs-to-be-negotiated-such-as-dp-2-lane-vs-dp-4-lane"></a>需要协商备用模式的操作系统输入，例如 DP 2 通道与 DP 4 通道

不是。 操作系统 (或任何 Microsoft 提供的软件组件) 在选择备用模式时不起作用。 该决策由连接器的驱动程序（具体而言就是 USB 连接器管理器 (UCM) 客户端驱动程序）决定。 驱动程序通过使用硬件接口与连接器的固件通信来实现此目的。

## <a name="pre-os-charging-with-type-c-and-pd"></a>类型 C 和 PD 的预操作系统收费

启用预操作系统收费由 OEM 所有。 你可以选择不实现 [Usb 电源交付](https://www.usb.org/usb-charger-pd)，并按 USB 类型-C 电源级别收费，直到启动到操作系统为止。

## <a name="charging-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum"></a>在电话为 USB 主机时对电话进行收费，以启用扩展方案，例如 Continuum

下面是一些需要考虑的事项：

- 必须实现 [USB 电源交付](https://www.usb.org/usb-charger-pd)，以便能够独立交换电源和数据角色。
- 坞站的上游端口应作为收费 UFP 来实现，这是在 USB 类型 C 规范中定义的。 有关详细信息，请参阅4.8.4 版本1.1。
- 如果你的停靠解析到 DFP，则应请求一个 DR \_ 交换， \_ 如果它解析为 UFP，则应请求一个 PR 交换。

  初始 DFP 是电源，因此必须更改数据角色。 初始 UFP 是电源接收器，因此必须更改电源角色。 您可以在以下回调函数的实现中执行这些操作：

## <a name="windows-10-mobile-support-of-usb-billboard-devices"></a>USB 布告栏设备的 Windows 10 移动版支持

是的，如果将手机连接到支持 USB 布告栏的设备，根据 [布告栏设备规范的 Usb 设备类定义](https://www.usb.org/document-library/billboard-device-class-spec-revision-121-and-adopters-agreement#:~:text=The%20USB%20Billboard%20Device%20Class%20definition%20describes%20the,to%20provide%20support%20details%20in%20a%20human-readable%20format.)，会通知用户。 USB 连接器管理器 (UCM) 客户端驱动程序无需处理通知。 如果系统无法识别备用模式，请不要进入该模式。

## <a name="support-for-usb-type-c-on-earlier-versions-of-windows"></a>在早期版本的 Windows 上支持 USB 类型 C

在 Windows 10 之前的 Windows 版本中不支持 USB 类型 C。

## <a name="ucsi-support-on-earlier-versions-of-windows"></a>Windows 早期版本上的 UCSI 支持

Windows 10 之前的 Windows 版本不支持 UCSI。

## <a name="how-to-test-an-implementation-of-ucsi"></a>如何测试 UCSI 的实现

若要测试你的实现，请遵循 [USB 类型 C 手动互操作性测试过程](type.md)中提供的指导原则。 建议在适用于 Windows 10 (HLK) 的 Windows 硬件实验室包中运行 USB 测试。 这些测试在适用于 [USB 的 Windows 硬件认证包测试](windows-hardware-certification-kit-tests-for-usb.md)中列出。

## <a name="conditions-and-ui-for-the-different-errors"></a>不同错误的条件和 UI

Windows 10 可以显示一组 USB 类型 C 错误消息，以帮助用户了解有关 USB 类型 C 硬件和软件的不同组合的限制。 例如，如果连接到 USB 类型 C 连接器的充电器的功能不足、与系统不兼容，或连接到非充电端口，则用户可能会收到 "设备充电缓慢" 消息。 有关详细信息，请参阅 [有关 USB 类型 C Windows 系统的消息疑难解答](https://support.microsoft.com/windows/fix-usb-c-problems-f4e0e529-74f5-cdae-3194-43743f30eed2#devicenotwork)。

## <a name="connecting-a-non-pd-port-to-a-pd-provider-and-a-pd-consumer-to-a-system-that-is-not-a-pd-provider"></a>将非 PD 端口连接到 PD 提供程序，将 PD 使用者连接到不是 PD 提供程序的系统

非 PD 端口尝试使用 USB 类型 C 当前级别对系统进行计费。 有关详细信息，请参阅 [usb 3.1 和 Usb Type-C 规范](https://www.usb.org/usb-type-cr-cable-and-connector-specification)。

## <a name="connecting-thunderbolt-supermhl-or-pci-express-to-a-pc-that-does-not-support-those-capabilities"></a>将闪电、SuperMHL 或 PCI express 连接到不支持这些功能的电脑

备用模式功能允许 (的非 USB 协议，如闪电、SuperMHL) 通过 USB 电缆运行，同时保留 USB 2.0 和充电功能。 如果用户连接的 USB 类型为 C 的备用模式设备或适配器不受连接的 PC 或运行 Windows 10 的电话支持，则会检测到一个错误情况并向用户显示一条消息。

- 如果设备或适配器公开了布告栏设备，则用户将看到有关错误条件的信息，以帮助解决问题。 Windows 10 提供了一个用于布告栏设备的内置驱动程序，并通知用户出现了错误。
- 用户可能会看到错误通知 "尝试改善 USB 连接"。 有关详细信息，请参阅 [修复 USB-C 问题](/windows/fix-usb-c-problems-f4e0e529-74f5-cdae-3194-43743f30eed2)。

为获得最佳结果，请确保电脑或电话或电缆满足备用模式设备或适配器的要求。

## <a name="support-and-limitations-for-mtp-over-usb-type-c-in-windows"></a>Windows 中通过 USB 类型 C 进行 MTP 的支持和限制

适用于桌面版的 Windows 10 支持 "发起方" 角色中的 MTP;Windows 10 移动版支持响应方角色中的 MTP。

## <a name="how-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm"></a>下游设备和集线器如何连接并与 USB 连接器管理器通信 (UCM) 

UCM 是其自身的设备堆栈 (参阅 [体系结构：用于 Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)) 。 Windows 10 对 USB 类型-C 的支持包括所需的管道，以确保不同的类驱动程序知道如何与不同的 USB 类型 C 连接器通信。 若要为 USB 类型 C 获取 Windows 10 支持，必须插入到 UCM 设备堆栈中。

## <a name="usb-type-c-mutt-requirements-for-hlk-tests"></a>针对 HLK 测试的 USB 类型-C MUTT 要求

适用于 Windows 10 的 Windows HLK 包含 USB 主机和函数控制器的测试。 若要测试您的系统，请使用 USB C-A 适配器。 这些测试在适用于 [USB 的 Windows 硬件认证包测试](windows-hardware-certification-kit-tests-for-usb.md)中列出。

## <a name="microsoft-support-for-p2p-data-transfer-between-the-same-windows-10-sku"></a>Microsoft 对同一 Windows 10 SKU 之间的 P2P 数据传输的支持

这不是有效的连接。

- 对于桌面版，不能连接两台运行 Windows 10 的电脑。
- 不能连接运行 Windows 10 移动版的两个移动设备。

如果用户尝试建立此类连接，Windows 将显示一条错误消息。 有关详细信息，请参阅 [USB 类型 C Windows 系统的错误消息](introduction-to-usb-type-c-connectors.md#-6)。

唯一有效的连接是在 Windows 移动设备和 Windows 桌面设备之间。

## <a name="ucm-class-extension-ucmcx-communication-with-pmic-or-battery-driver-to-getset-charging-status"></a>UCM class extension (UcmCx) 与 PMIC 或电池驱动程序通信，以获取/设置充电状态

在软件辅助充电平台上，UcmCx 与 PMIC 和电池子系统通信。 客户端驱动程序可以通过硬件接口与硬件通信来确定充电级别。 在硬件辅助平台上，嵌入式控制器负责充电。 在此过程中，UcmCx 不会执行任何操作。

## <a name="hlk-support-for-usb-type-c"></a>对 USB 类型 C 的 HLK 支持

在适用于 Windows 10 的 Windows HLK 中，没有 USB 类型 C 特定的测试。 建议在适用于 Windows 10 的 Windows HLK 中运行 USB 测试。 这些测试在适用于 [USB 的 Windows 硬件认证包测试](windows-hardware-certification-kit-tests-for-usb.md)中列出。

## <a name="ucsi"></a>UCSI

[Usb 类型-c 连接器系统软件接口 (UCSI) 规范](https://www.intel.com/content/www/us/en/products/docs/io/universal-serial-bus/usb-type-c-ucsi-spec.html) 介绍了 USB C # 连接器系统软件接口 (UCSI) 的功能，并说明了硬件组件设计器、系统构建者和设备驱动程序开发人员的寄存器和数据结构。

Microsoft 提供内置驱动程序和 Windows UcmUcsi.sys，该驱动程序实现了该规范所定义的功能。 此驱动程序适用于具有嵌入式控制器的系统。

## <a name="test-a-ucsi-implementation-running-on-windows-10"></a>测试 Windows 10 上运行的 UCSI 实现

建议在适用于 Windows 10 的 Windows HLK 中运行 USB 测试。 这些测试在适用于 [USB 的 Windows 硬件认证包测试](windows-hardware-certification-kit-tests-for-usb.md)中列出。

## <a name="test-a-ucmcx-client-driver-on-windows-10"></a>在 Windows 10 上测试 UCMCx 客户端驱动程序

建议在适用于 Windows 10 的 Windows HLK 中运行 USB 测试。 这些测试在适用于 [USB 的 Windows 硬件认证包测试](windows-hardware-certification-kit-tests-for-usb.md)中列出。

## <a name="vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension"></a>UCM 类扩展处理的 VBus/VConn 控件和角色切换操作

UCM 类扩展可能会从操作系统获取请求，以更改连接器的数据或电源方向。 当它获取这些请求时，它会调用客户端驱动程序的 [* \_ UCM \_ 连接器 \_ 集 \_ 数据 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role) 和 [*.evt \_ UCM \_ 连接器 \_ 集 \_ 电源 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role) 回调函数的实现， (如果连接器实现了 PD) 。 在实现中，客户端驱动程序应该控制 VBUS 和 VCONN 的 pin。 有关这些回调函数的详细信息，请参阅 [编写 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)。
