---
Description: The USBLPM tool monitors the U0/U1/U2/U3 power states of USB 3.0 ports.
title: USBLPM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b78f84cda3a74955ae1861f093e95731fc841c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576611"
---
# <a name="usblpm"></a>USBLPM


USBLPM 工具监视 USB 3.0 端口 U0/U1/U2/U3 电源的状态。 此外可以用于验证正确发生 U0/U1/U2 之间的转换。 此外，该工具可以启用或禁用系统中的所有设备上的 U1 和/或 U2 状态。

该工具包含在[MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)。

## <a name="usblpm"></a>USBLPM


USBLPM 仅适用于 Windows 8 和适用于 Microsoft USB 3.0 驱动程序堆栈。 该工具不运行批处理文件和此包中的脚本的一部分。 该工具的控制器、 中心和设备的公司用于监视新的 USB 3.0 电源状态。

在运行 USBLPM**监视**，**测试**，或**配置**模式。

![usb lpm 工具](images/fig10-usb-lpm-tool.png)

### <a name="monitoring"></a>监视

不带任何参数运行该工具时，这是默认模式。 在此模式下，此工具定期查询每个级别的 USB 3.0 设备并显示当前 U 状态的端口。 默认情况下，该工具每隔 500 毫秒运行查询。

在监视模式中，可以通过此命令行选项更改的期：

**usblpm /PollingInterval** &lt;*时间以毫秒为单位*&gt;

其中的时间值是一个介于 1 和 100000 之间。 **/PollingInterval**选项是可选的。 一般情况下，不应更改的时间段。

### <a name="testing"></a>正在测试

**若要测试的设备或中心：**

1.  启动该工具。
2.  测试监视中更改的模式。
3.  选择测试设备。
4.  单击**启动**启动测试运行。

在 10 秒内完成测试并向用户显示结果。

在测试尝试 U0/U1/U2 状态的不同组合，并确保，在测试设备重新进入 U0 成功。 可通过发送控制传输其查询 BOS 描述符。

若要测试集线器，删除附加到它的所有设备并运行测试。 然后，将一个或多个设备连接并重新运行测试。 但是，如果下游设备之一不正确地支持 U1/U2，中心测试失败。 因此，中心上的测试之前，我们建议中心以确保它们通过的测试的下一级的设备在首次运行测试。

**请注意**  运行测试时不更改设备拓扑。 如果动态更改配置，该工具的行为是未定义。

 

### <a name="configuring-u1u2-states"></a>配置 U1/U2 状态

USBLPM 可用于启用或禁用的系统上的所有 USB 设备的 U1 和 U2 状态通过运行以下命令：

**usblpm /enable | / 禁用 U1 |U2**

例如，此命令禁用 U2:

**usblpm /disable U2**

在配置模式下，该工具不显示任何窗口。 运行该工具后，将保留启用或禁用。

### <a name="known-issues-with-usblpm"></a>USBLPM 的已知的问题

测试选择性之前挂起 SuperSpeed 集线器，应执行以下步骤来禁用选择性挂起。

1.  在设备管理器中，右键单击**SuperSpeed 集线器**，然后选择**属性**。
2.  单击**电源管理**选项卡。
3.  取消选中**允许计算机关闭此设备以节约电源**。

使用 USBLPM 测试完成后，启用选择性挂起的中心通过检查**允许计算机关闭此设备以节约电源以重新启用选择性挂起**。

**请注意**  USBLPM 当前不会测试 USB 2.1 LPM。

 

## <a name="related-topics"></a>相关主题
[USB 测试工具](usb-test-tools.md)  
[MUTT 软件包中的工具](mutt-software-package.md)  



