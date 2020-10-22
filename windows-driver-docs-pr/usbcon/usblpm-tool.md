---
description: USBLPM 工具监视 USB 3.0 端口的 U0/U1/U2/U3 电源状态。
title: USBLPM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd34192745e6dbabd1c97ccb9887ec7ca547d705
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356037"
---
# <a name="usblpm-tool"></a>USBLPM 工具

USBLPM 工具监视 USB 3.0 端口的 U0/U1/U2/U3 电源状态。 它还可用于验证 U0/U1/U2 之间的转换是否正常进行。 此外，该工具可以启用或禁用系统中所有设备上的 U1 和/或 U2 状态。

该工具包含在 [MUTT](./index.md)软件包中。

## <a name="usblpm"></a>USBLPM

USBLPM 仅适用于 Windows 8，适用于 Microsoft USB 3.0 驱动程序堆栈。 此工具不作为此包中的批处理文件和脚本的一部分运行。 该工具适用于控制器、集线器和设备公司，用于监视新的 USB 3.0 电源状态。

USBLPM 在 **监视**、 **测试**或 **配置** 模式下运行。

![usb lpm 工具](images/fig10-usb-lpm-tool.png)

### <a name="monitoring"></a>监视

如果没有任何参数的情况下运行该工具，则这是默认模式。 在此模式下，该工具会定期查询每个级别的 USB 3.0 设备，并显示端口的当前 U 状态。 默认情况下，该工具每500毫秒运行一次查询。

在监视模式下，可以通过此命令行选项更改句点：

```console
usblpm /PollingInterval &lt;*time in milliseconds*&gt;
```

其中，时间值是从1到100000的整数。 **/PollingInterval**选项是可选的。 通常，不应更改时间段。

### <a name="testing"></a>测试

**若要测试设备或集线器：**

1. 启动工具。
2. 将模式从监视更改为测试。
3. 选择测试设备。
4. 单击 " **启动** " 以启动测试运行。

测试在10秒内完成，并向用户显示结果。

测试尝试 U0/U1/U2 状态的不同组合，并确保测试设备重新进入 U0。 这是通过发送查询 BOS 描述符的控制传输来完成的。

若要测试集线器，请删除附加到它的所有设备并运行测试。 然后，附加一个或多个设备并重新运行测试。 但是，如果其中一个下游设备不能正确支持 U1/U2，则中心测试将失败。 因此，在中心运行测试之前，建议先在中心下游的设备上运行测试，以确保它们通过测试。

> [!NOTE]
>请不要在运行测试时更改设备拓扑。 如果动态更改了配置，则该工具的行为不确定。

### <a name="configuring-u1u2-states"></a>配置 U1/U2 状态

可以通过运行以下命令，使用 USBLPM 为系统上的所有 USB 设备启用或禁用 U1 和 U2 状态：

```console
usblpm /enable|/disable U1|U2
```

例如，以下命令将禁用 U2：

```console
usblpm /disable U2
```

在配置模式下，该工具不会显示任何窗口。 运行该工具后，启用或禁用将保持不变。

### <a name="known-issues-with-usblpm"></a>USBLPM 的已知问题

在为 SuperSpeed 中心测试选择性挂起之前，应执行以下步骤来禁用选择性挂起。

1. 在设备管理器中，右键单击 **SuperSpeed 中心** ，然后选择 " **属性**"。
2. 单击 " **电源管理** " 选项卡。
3. 取消选中 **"允许计算机关闭此设备以节省电源"**。

使用 USBLPM 完成测试后，通过选中 " **允许计算机关闭此设备以节省电源" 以重新启用选择性挂起**，为中心启用选择性挂起。

> [!NOTE]
> USBLPM 当前未测试 USB 2.1 LPM。

## <a name="related-topics"></a>相关主题

[Microsoft USB 测试工具 (MUTT) 设备的概述](/windows-hardware/drivers/usbcon/microsoft-usb-test-tool--mutt--devices)

[MUTT 软件包中的工具](mutt-software-package.md)
