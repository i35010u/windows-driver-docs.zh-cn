---
Description: 适用于在构建 USB 类型 C 的系统的 Oem 支持 USB C 型连接器和任务的 Windows。
title: Windows 对 USB 类型 C 连接器的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4cca50437de9aadbcd65be59bfbdf75042e1fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368832"
---
# <a name="windows-support-for-usb-type-c-connectors"></a>Windows 对 USB 类型 C 连接器的支持

本主题适用于想要构建 Windows 10 的系统，使用 USB C 型连接器，并且想要利用操作系统功能，通过宣传位置设备能够更快地收费、 power 交付、 双角色、 备用模式和错误通知的 Oem。

传统的 USB 连接与每一端上的 USB A 和 B USB 连接器使用电缆。 USB A 连接器始终在主机端到插入和 USB B 连接器连接函数端，这是设备 （电话） 或外围设备 （鼠标、 键盘）。 通过使用这些连接器，你只能连接到一个函数; 的主机永远不会主机到另一台主机或另一个函数的函数。 主机是电源的源提供程序，该函数使用来自主机电源。

传统配置限制某些情况。 例如，如果移动设备要连接到外围设备，设备必须充当主机并传递到已连接设备的电源。

引入了 USB 的 USB 类型 C 连接器-如果 USB 3.1 规范中定义，解决这些限制。 Windows 10 引入了对这些功能的本机支持。

![usb 连接器比较](images/typecccomp.jpg)


## <a name="feature-summary"></a>功能摘要

- 允许针对更快地向收费 100W 到与电源传递通过 USB 类型。
- 有关 USB 主机和 USB 设备的单个连接器。
- 可以切换 USB 角色，以支持 USB 主机或设备。
- 可以切换源和接收电源之间 power 角色。
- 支持其他协议，如 DisplayPort 和闪电通过 USB 类型。
- 引入了 USB 布告栏设备类以提供其他模式的错误通知。

**正式规范**

[USB 3.1 和 USB 类型 C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)

[USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)

[宣传位置设备规范](https://go.microsoft.com/fwlink/p/?linkid=620207)

[UCSI 规范](https://go.microsoft.com/fwlink/p/?LinkId=703713)

## <a name="hardware-design"></a>硬件设计
USB C 型连接器是可还原和对称。

![USB 类型 C 对称电缆](images/usb-type-c.png)

主要组件是： USB 类型 C 连接器及其端口或管理连接器的抄送 pin 逻辑 PD 控制器。 此类系统通常有可以交换 USB 角色从主机到函数的双角色控制器。 它具有显示扩展模块，允许在通过 USB 传输的视频信号。 （可选） 它可以支持 BC1.2 充电器检测。

- [USB C 类型系统的硬件设计](architecture--usb-type-c-in-a-windows-system.md)
- [与嵌入式控制器 USB C 类型系统的硬件设计](ucsi.md)

请考虑的设计和开发的 USB 组件，包括最低硬件要求、 Windows 硬件兼容性计划要求和基于这些要求的其他建议的建议。
[硬件组件指南 USB](https://docs.microsoft.com/windows-hardware/design/component-guidelines/universal-serial-bus--usb-)

## <a name="choose-a-driver-model"></a>选择驱动程序模型

使用此流程图来确定您的 USB C 类型系统的解决方案。 
![驱动程序](images/drivers-c.png)

|如果您的系统...| 建议的解决方案...|
|---|---|
|未实现 PD 状态机 |写入 UcmTcpciCx 类扩展客户端驱动程序。 <p>[写入 USB 类型 C 端口控制器驱动程序](write-a-usb-type-c-port-controller-driver.md)</p>|
|实现 PD 状态中的硬件或固件的计算机，并通过 ACPI 支持 USB 类型 C 连接器系统软件接口 (UCSI)| 加载 Microsoft 提供的现成驱动程序，UcmUcsiCx.sys 和 UcmUcsiAcpiClient.sys。 <p>请参阅[UCSI 驱动程序](ucsi.md)。</p>|
|实现 PD 状态机中的硬件或固件，但不能支持 UCSI，或者支持 UCSI 但需要非 ACPI 传输|编写 UcmCx 类扩展的客户端驱动程序。<p>[编写 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)</p><p>[编写 USB 类型 C 策略管理器客户端驱动程序](policy-manager-client.md)</p>|
|实现 UCSI，但需要非 ACPI 传输|写入 UcmUcsiCx 类扩展客户端驱动程序。<p>使用[此示例模板](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)并修改它基于您的硬件使用的传输。</P><p>[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)</P>|


## <a name="bring-up-drivers"></a>显示驱动程序

- USB 函数驱动程序启动，才需要如果支持 USB 功能模式。 如果您以前实现 USB micro B 连接器的 USB 函数驱动程序，描述相应连接器 USB 类型-C 作为 USB 功能驱动程序以继续工作的 ACPI 表中。 

    有关详细信息，请参阅[有关编写 USB 功能驱动程序的说明](developing-windows-drivers-for-usb-function-controllers.md)。

- USB 角色切换驱动程序启动，才需要具有双角色控制器充当主机和函数角色的设备。 若要启动的 USB 角色切换驱动程序，您需要修改 ACPI 表以启用 Microsoft 中现成 USB 角色切换驱动程序。 

    有关详细信息，请参阅[USB 角色交换机驱动程序提供的指南](dual-role-controller-bringup-for-a-usb-type-c-system.md)。

- USB 连接器管理器驱动程序是必需的 Windows 管理的系统上的 USB 类型 C 端口。 USB 连接器管理器驱动程序的自带向上任务取决于你为 USB 类型 C 端口选择的驱动程序：Microsoft 中现成 UCSI （UcmUcsiCx.sys 和 UcmUcsiAcpiClient.sys） 驱动程序、 UcmCx 客户端驱动程序或 UcmTcpciCx 客户端驱动程序。 有关详细信息，请参阅介绍如何选择适当的解决方案为您的 USB C 类型系统中的前面部分的链接。


## <a name="test"></a>测试
执行各种功能和压力测试系统和设备公开 USB 类型 C 连接器上。

[测试与 USB 类型 C ConnEx USB 类型 C 系统](test-usb-type-c-systems-with-mutt-connex-c.md)-包括适用于 Windows 10 的 Windows 硬件 Lab Kit (HLK) 中运行 USB 测试。
> 运行的 USB 函数 HLK 测试与 C 到 A 电缆 (搜索**Windows USB 设备**HLK 中 

符合性认证/参加 Power 交付和 USB 类型 C 标准主体由托管的符合性研讨会。
 
## <a name="see-also"></a>请参阅


-   [常见问题解答：Windows 系统上的 USB C 型连接器](faq--usb-type-c-connector-on-a-windows-system.md)
-   [在用户界面中的消息疑难解答](https://go.microsoft.com/fwlink/?LinkId=526894) 

 




