---
Description: Microsoft USB 测试工具 (MUTT) 是用于测试您的 USB 硬件与 Microsoft USB 驱动程序堆栈的互操作性的设备的集合。
title: Microsoft USB 测试工具 (MUTT) 设备的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ce3a2d372588aa0682e79e0e20fd0ed1fe93459
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717006"
---
# <a name="overview-of-microsoft-usb-test-tool-mutt-devices"></a>Microsoft USB 测试工具 (MUTT) 设备的概述


**摘要**

-   MUTT 设备的说明
-   本部分中列出的制造商出售 MUTT 运行互操作性测试所需的硬件看板。
-   [![下载 mutt 软件包](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)MUTT 软件包，以获取最新版本的测试工具。

Microsoft USB 测试工具 (MUTT) 是用于测试您的 USB 硬件与 Microsoft USB 驱动程序堆栈的互操作性的设备的集合。 本部分提供了不同类型的 MUTT 设备、 测试可以运行使用该设备，并建议的控制器、 中心、 设备、 拓扑和 BIOS/UEFI 测试的简要概述。

若要与 MUTT 设备进行通信，需要 MUTT 软件包。 此包包含多个测试工具和让测试工程师测试互操作性 USB 控制器或与 Microsoft USB 驱动程序堆栈的中心的硬件的驱动程序。 测试工具验证 USB 主机控制器软件、 硬件 （包括固件） 和任何已安装主控制器和设备之间的 USB 集线器。

## <a name="how-to-get-mutt-devices"></a>如何获取 MUTT 设备


<a href="" id="mutt"></a>MUTT  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-pack"></a>MUTT 包  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="supermutt"></a>SuperMUTT  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

[Pactron](http://pactronstore.com/products/supermutt.mdl)

<a href="" id="supermutt-pack"></a>SuperMUTT 包  
[通过实验室](https://go.microsoft.com/fwlink/p/?linkid=618285)

<a href="" id="dr-mutt"></a>DR MUTT  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-connex-c"></a>USB 类型 C ConnEx [MCCI](https://go.microsoft.com/fwlink/p/?LinkId=733488)

[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

## <a name="mutt"></a>MUTT


-   基于 CY3681 EZ USB FX2 开发工具包 (Cypress FX2) 的设计。
-   与兼容**FX2**功能，如高速度和全速传输到大容量、 等时，控制中断终结点。
-   模拟从 USB 2.0 设备的流量。

    ![mutt 设备](images/fig1-mutt-device.png)

## <a name="mutt-pack"></a>MUTT 包


MUTT 包是一个 USB 2.0 集线器和控制中心，并充当下游设备的 FX2 设备的组合。

-   基于上 Cypress 中心和 Cypress FX2 设计。
-   中心功能。 这可以充当多 TT 或单 TT 高速集线器;模拟过电流。
-   显示可以打开或关闭的下游端口。
-   模拟 USB 2.0 中心的行为。
-   可以在自供电或总线供电模式下运行。

    ![mutt 包设备](images/fig2-muttpackdevice.png)

MUTT 包都具有两个 USB 连接器。 标准 B 连接器用于插入 MUTT 包到主机系统中。 标准版连接器的 MUTT 包上的嵌入中心的下游和可用于其他设备测试 （在本文档后面讨论）。

![mutt pack 连接器](images/fig3-muttpackconnectors.png)

### <a name="how-to-power-the-mutt-pack"></a>如何对 power MUTT 包

MUTT 包使用小跳线 （见图 3） 自供电和总线驱动模式之间切换。 在总线供电的模式下，主机系统的 USB 总线为 MUTT Pack 提供支持。 在自供电模式下，MUTT 包与外部 5V 电源适配器提供支持。

![mutt 包功耗流程图](images/fig4-muttpackpoweringflowchart.png)

使用以下流程图来确定如何 power MUTT 包：

**请注意**  不使用而无需 power 跳线 MUTT 包。

 

![不正确的用法](images/fig5-muttpackincorrectusage.png)

此图显示了如何为主机系统的 USB 总线增强 MUTT 包使用跳线：

![mutt 包总线供电](images/fig6-muttpackbuspowered.png)

此图显示了如何使用跳线设置为与外部电源适配器增强 MUTT 包：

![mutt pack 自助支持](images/fig7-muttpackselfpowered.png)

**请注意**  时您要更改跳线上 MUTT 包断开连接的任何现有电源适配器和电缆连接到主机系统。

 

## <a name="supermutt"></a>SuperMUTT


-   基于 FX3 EZ USB FX3 的设计。
-   实现 SuperSpeed 功能，如大容量流功能。
-   模拟 USB 3.0 设备的流量。
-   注意： 此设备不支持在低速度的操作。

    ![supermutt](images/fig8-supermutt.png)

## <a name="supermutt-pack"></a>SuperMUTT 包


SuperMUTT 包是一个中的两个设备。 它是与 Cypress FX2 下游设备的 USB 3.0 集线器。 设备控制中心，并且还可作为下游设备。 该 SuperMUTT 包模拟 USB 3.0 集线器行为。

**请注意**  下游设备是 2.0 设备，而不是 USB 3.0 设备。

 

![supermutt 包](images/supermuttpack.png)

## <a name="dr-mutt"></a>DR MUTT


DR MUTT 像 supermutt 后测试待测试设备的主机模式时，但它还可以切换到要测试待测试设备的功能模式下的主机模式。

## <a name="usb-type-c-connex"></a>USB 类型 C ConnEx


USB 类型 C 连接试验程序 (USB 类型 C ConnEx) 是具有四个开关来自动执行 USB 类型 C 互操作性方案的自定义防护罩。 防护罩已被用于处理与 arduino 配合使用作为微型控制器。 有关详细信息，请参阅[测试 USB 类型-C 系统与 USB 类型 C ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md)。

![USB 类型 C ConnEx](images/connexc-side.jpg)

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[在 Windows 中测试 USB 硬件、 驱动程序和应用程序](usb-driver-testing-guide.md)  




