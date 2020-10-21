---
description: Windows 支持 USB 类型 C 连接器和用于构建 USB 类型 C 系统的 Oem 的任务。
title: Windows 对 USB 类型 C 连接器的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d50602a2386454258a2127a47ea58fb0935a8023
ms.sourcegitcommit: b75e9940d49410e2b952e96f325df67a039cd571
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92337054"
---
# <a name="windows-support-for-usb-type-c-connectors"></a>Windows 对 USB 类型 C 连接器的支持

本主题适用于想要使用 USB 类型 C 连接器构建 Windows 10 系统的 Oem，并想要利用允许通过布告栏设备进行更快收费、电源交付、双重角色、备用模式和错误通知的操作系统功能。

传统 USB 连接在每一端使用带有 USB A 和 USB B 连接器的电缆。 USB A 连接器始终插入主机端，而 USB B 连接器连接函数端，这是一个设备 (电话) 或外围 (鼠标、键盘) 。 通过使用这些连接器，只能将主机连接到一个函数;永远不要将主机到另一台主机或函数。 主机是电源提供程序，函数消耗主机的电源。

传统配置限制了某些情况。 例如，如果移动设备要连接到外围设备，则设备必须充当主机并为连接的设备提供电源。

Usb 3.1 规范中定义的 usb C # C # 连接器会解决这些限制。 Windows 10 引入了对这些功能的本机支持。

![usb 连接器比较](images/typecccomp.jpg)

## <a name="feature-summary"></a>功能摘要

- 通过 USB 类型 C 上的 Power 交付，允许更快地充电到100W。
- 用于 USB 主机和 USB 设备的单一连接器。
- 可以切换 USB 角色以支持 USB 主机或设备。
- 可以在源和接收电源之间切换电源角色。
- 支持其他协议，如 DisplayPort 和闪电 over USB Type-C。
- 介绍 USB 布告栏设备类，以便为备用模式提供错误通知。

## <a name="official-specifications"></a>官方规范

[USB 类型-C 规范](https://usb.org/document-library/usb-type-cr-cable-and-connector-specification-revision-20)

[USB 电源交付](https://www.usb.org/sites/default/files/D2T2-1%20-%20USB%20Power%20Delivery.pdf)

[布告栏设备规范](https://www.usb.org/document-library/billboard-device-class-spec-revision-121-and-adopters-agreement#:~:text=The%20USB%20Billboard%20Device%20Class%20definition%20describes%20the,to%20provide%20support%20details%20in%20a%20human-readable%20format.)

[UCSI 规范](https://www.intel.com/content/www/us/en/products/docs/io/universal-serial-bus/usb-type-c-ucsi-spec.html)

## <a name="hardware-design"></a>硬件设计

USB 类型 C 连接器是可逆的并且对称。

![USB 类型-C 对称电缆](images/usb-type-c.png)

主要组件是： USB C # 连接器及其端口或 PD 控制器，用于管理连接器的 CC pin 逻辑。 此类系统通常具有一个双重角色控制器，可将 USB 角色从主机交换到功能。 它有 Display-Out 模块，允许通过 USB 传输视频信号。 也可以支持 BC 1.2 充电器检测。

- [USB 类型 C 系统的硬件设计](architecture--usb-type-c-in-a-windows-system.md)
- [使用嵌入式控制器的 USB 类型 C 系统的硬件设计](ucsi.md)

考虑用于设计和开发 USB 组件的建议，包括最低硬件要求、Windows 硬件兼容性计划要求以及根据这些要求构建的其他建议。
[硬件组件准则 USB](/windows-hardware/design/component-guidelines/universal-serial-bus--usb-)

## <a name="choose-a-driver-model"></a>选择驱动程序模型

使用此流程图确定 USB 类型 C 系统的解决方案。
![驱动程序](images/drivers-c.png)

|如果你的系统 .。。| 推荐的解决方案 .。。|
|---|---|
| 不实现 PD 状态机 | 将客户端驱动程序写入 UcmTcpciCx 类扩展。</br></br>[编写 USB 类型 C 端口控制器驱动程序](write-a-usb-type-c-port-controller-driver.md) |
| 在硬件或固件中实现 PD 状态机并支持 USB 类型-C 连接器系统软件接口 (UCSI) over ACPI | 加载 Microsoft 提供的内置驱动程序、UcmUcsiCx.sys 和 UcmUcsiAcpiClient.sys。</br></br>请参阅 [UCSI 驱动程序](ucsi.md)。 |
| 在硬件或固件中实现 PD 状态的计算机，但不支持 UCSI 或支持 UCSI，但要求使用除 ACPI 以外的其他传输 | 编写 UcmCx 类扩展的客户端驱动程序。</br></br>[编写 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)</br></br>[编写 USB 类型 C 策略管理器客户端驱动程序](policy-manager-client.md) |
| 实现 UCSI，但需要除 ACPI 以外的其他传输 | 将客户端驱动程序写入 UcmUcsiCx 类扩展。</br></br>使用 [此示例模板](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi) ，并根据硬件使用的传输来修改它。</br></br>[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md) |

## <a name="bring-up-drivers"></a>启动驱动程序

- 只有在支持 USB 功能模式时，才需要 USB 函数驱动程序。 如果先前为 USB 微 B 连接器实现了 USB 函数驱动程序，请在 ACPI 表中将相应的连接器描述为 usb 类型 C，以使 USB 功能驱动程序继续工作。

    有关详细信息，请参阅 [有关编写 USB 函数驱动程序的说明](developing-windows-drivers-for-usb-function-controllers.md)。

- 只有具有双重角色控制器的设备需要同时采用主机角色和函数角色，才能使用 USB Role-Switch 驱动程序。 若要打开 USB Role-Switch 驱动程序，需要修改 ACPI 表以启用 Microsoft 内置 USB 角色切换驱动程序。

    有关详细信息，请参阅 [用于启动 USB 角色切换驱动程序的指南](dual-role-controller-bringup-for-a-usb-type-c-system.md)。

- Windows 需要使用 USB 连接器管理器驱动程序来管理系统上的 USB 类型 C 端口。 USB 连接器管理器驱动程序的启动任务取决于你为 USB 类型 C 端口选择的驱动程序： Microsoft 内置 UCSI ( # A0 和 UcmUcsiAcpiClient.sys) 驱动程序，UcmCx 客户端驱动程序，或 UcmTcpciCx 客户端驱动程序。 有关详细信息，请参阅上一节中的链接，其中描述了如何为 USB 类型 C 系统选择正确的解决方案。

## <a name="test"></a>测试

在公开 USB C # C 连接器的系统和设备上执行各种功能和压力测试。

[测试 Usb 类型 c 系统和 Usb 类型-c ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md) -运行 Windows 硬件实验室工具包中包含的包含在 windows 10 (HLK) 的 usb 测试。
> 使用 C 对电缆运行 USB 函数的 HLK 测试 (在 HLK 中搜索**WINDOWS USB 设备**

认证/合规性会参加由标准机构托管的电源交付和 USB 类型 C 符合性研讨会。

## <a name="see-also"></a>另请参阅

- [常见问题解答：Windows 系统上的 USB 类型 C 连接器](faq--usb-type-c-connector-on-a-windows-system.md)
- [UI 中的消息疑难解答](https://support.microsoft.com/windows/fix-usb-c-problems-f4e0e529-74f5-cdae-3194-43743f30eed2#devicenotwork)
