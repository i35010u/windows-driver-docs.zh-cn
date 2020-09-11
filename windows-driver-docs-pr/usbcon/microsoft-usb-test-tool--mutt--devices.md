---
description: Microsoft USB 测试工具 (MUTT) 是设备的集合，用于测试 USB 硬件与 Microsoft USB 驱动程序堆栈之间的互操作性。
title: Microsoft USB 测试工具 (MUTT) 设备的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a826877933940a50fd90e8112da395c500eb2a3
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010285"
---
# <a name="overview-of-microsoft-usb-test-tool-mutt-devices"></a>Microsoft USB 测试工具 (MUTT) 设备的概述


**摘要**

-   MUTT 设备的说明
-   本部分中所列的制造商销售运行互操作性测试所需的 MUTT 硬件板。
-   [ ![ 下载 MUTT](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)软件包 mutt 软件包以获取最新版本的测试工具。

Microsoft USB 测试工具 (MUTT) 是设备的集合，用于测试 USB 硬件与 Microsoft USB 驱动程序堆栈之间的互操作性。 本部分简要概述了不同类型的 MUTT 设备、可以使用设备运行的测试，并为控制器、集线器、设备和 BIOS/UEFI 测试建议了拓扑。

若要与 MUTT 设备通信，需要 MUTT 软件包。 此包包含多个测试工具和驱动程序，使硬件测试工程师可以通过 Microsoft USB 驱动程序堆栈测试其 USB 控制器或集线器的互操作性。 测试工具将验证 USB 主机控制器软件、硬件 (包括固件) 和在主机控制器与设备之间安装的任何 USB 集线器。

## <a name="how-to-get-mutt-devices"></a>如何获取 MUTT 设备


<a href="" id="mutt"></a>MUTT  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-pack"></a>MUTT 包  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="supermutt"></a>SuperMUTT  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

[Pactron](https://pactronstore.com/products/supermutt.mdl)

<a href="" id="supermutt-pack"></a>SuperMUTT 包  
[通过实验室](https://go.microsoft.com/fwlink/p/?linkid=618285)

<a href="" id="dr-mutt"></a>DR MUTT  
[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-connex-c"></a>USB 类型-C ConnEx [MCCI](https://go.microsoft.com/fwlink/p/?LinkId=733488)

[JJG 技术]( https://go.microsoft.com/fwlink/p/?linkid=618287)

## <a name="mutt"></a>MUTT


-   根据 CY3681 EZ-USB FX2 开发工具包的设计， (Cypress FX2) 。
-   与 **FX2** 功能兼容，如高速和全速传输到大容量、同步、控制、中断端点。
-   模拟来自 USB 2.0 设备的流量。

    ![mutt 设备](images/fig1-mutt-device.png)

## <a name="mutt-pack"></a>MUTT 包


MUTT Pack 是 USB 2.0 集线器和 FX2 设备的组合，用于控制集线器并用作下游设备。

-   基于 Cypress 中心和 Cypress FX2 上的设计。
-   集线器功能。 这可以作为多 TT 或单 TT 高速中心进行操作;模拟过流。
-   公开可以打开或关闭的下游端口。
-   模拟 USB 2.0 集线器的行为。
-   可在自行驱动模式或总线供电模式下运行。

    ![mutt pack 设备](images/fig2-muttpackdevice.png)

MUTT Pack 有两个 USB 连接器。 标准 B 连接器用于将 MUTT Pack 插入主机系统。 标准 A 连接器是 MUTT Pack 上嵌入的中心的下游，可用于本文档后面的其他设备测试 () 。

![mutt pack 连接器](images/fig3-muttpackconnectors.png)

### <a name="how-to-power-the-mutt-pack"></a>如何为 MUTT Pack 供电

MUTT Pack 使用小型跳线 (参阅图 3) ，在自驱动模式和总线驱动模式之间切换。 在总线驱动模式下，主机系统的 USB 总线为 MUTT Pack 提供支持。 在自行驱动模式下，MUTT Pack 使用外部5V 电源适配器提供支持。

![mutt pack 电源流程图](images/fig4-muttpackpoweringflowchart.png)

使用以下流程图确定如何为 MUTT Pack 供电：

**注意**   请勿使用带有 power 跳线的 MUTT Pack。

 

![用法不正确](images/fig5-muttpackincorrectusage.png)

此图显示了如何使用跳线通过主机系统的 USB 总线为 MUTT Pack 供电：

![已支持 mutt pack 总线](images/fig6-muttpackbuspowered.png)

此图显示了如何使用跳线通过外部电源适配器为 MUTT pack 供电：

![mutt pack 自助式](images/fig7-muttpackselfpowered.png)

**注意**   当你更改 MUTT Pack 上的跳线时，请断开任何现有的电源适配器与主机系统的连接。

 

## <a name="supermutt"></a>SuperMUTT


-   基于 FX3 EZ-USB FX3 的设计。
-   实现 SuperSpeed 功能，例如大容量流功能。
-   模拟 USB 3.0 设备流量。
-   注意：此设备不支持慢速操作。

    ![supermutt](images/fig8-supermutt.png)

## <a name="supermutt-pack"></a>SuperMUTT 包


SuperMUTT Pack 是其中的两个设备。 它是一个 Cypress FX2 设备下游的 USB 3.0 集线器。 设备控制集线器，还充当下游设备。 SuperMUTT Pack 模拟 USB 3.0 集线器的行为。

**注意**   下游设备是2.0 设备，而不是 USB 3.0 设备。

 

![supermutt 包](images/supermuttpack.png)

## <a name="dr-mutt"></a>DR MUTT


在测试所测试设备的主机模式时，DR MUTT 的行为类似于 SuperMutt，但它也可以切换到主机模式来测试所测试设备的函数模式。

## <a name="usb-type-c-connex"></a>USB 类型-C ConnEx


USB Type-c 连接试验 (USB Type-C ConnEx) 是一个自定义盾牌，具有四对一交换机，可自动执行 USB 类型 C 互操作方案。 此防护板旨在使用 Arduino 作为微控制器。 有关详细信息，请参阅 [测试 usb 类型 c 系统和 Usb 类型-c ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md)。

![USB 类型-C ConnEx](images/connexc-side.jpg)

## <a name="related-topics"></a>相关主题
[USB](../index.yml)  
[在 Windows 中测试 USB 硬件、驱动程序和应用程序](usb-driver-testing-guide.md)