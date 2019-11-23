---
Description: Microsoft 提供了与 USB 类型 C 连接器系统软件接口（UCSI）规范兼容的驱动程序。
title: USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: bb4c1969370147e8298eabd32aef3befb2cee2e6
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007631"
---
# <a name="usb-type-c-connector-system-software-interface-ucsi-driver"></a>USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序


**摘要**

-   Microsoft 提供的内置 UCSI 驱动程序，适用于带有嵌入式控制器的 USB 类型 C 系统。

**上次更新时间**

-   2018 年 10 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

**官方规范**

-   [UCSI 的 Intel BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 类型-C 连接器系统软件接口规范](https://go.microsoft.com/fwlink/p/?LinkId=703713)
-   [硬件设计：适用于带有嵌入式控制器的系统的 USB 类型 C 组件](hardware-design-of-a-usb-type-c-system.md#emb)


Microsoft 为 ACPI 传输提供与 USB 类型 C 连接器系统软件接口（UCSI）规范兼容的驱动程序。 如果你的设计包含带有 ACPI 传输的嵌入式控制器，请在系统的 BIOS/EC 中实现 UCSI，并加载内置的 UCSI 驱动程序（UcmUcsiCx 和 UcmUcsiAcpiClient）。

如果 UCSI 兼容硬件使用的是非 ACPI 传输，则需[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)。

## <a name="drivers-for-supporting-usb-type-c-components-for-systems-with-embedded-controllers"></a>用于支持带嵌入式控制器的系统的 USB 类型 C 组件的驱动程序

下面是一个具有嵌入式控制器的系统的示例。

![usb 类型 c 软件组件](images/ucsiarch.png)

在前面的示例中，USB 角色切换在系统的固件中进行处理，并且未加载 USB 角色切换驱动程序堆栈。 在另一个系统中，可能无法加载驱动程序堆栈，因为不支持双重角色。

在上图中，

-   **USB 设备端驱动程序**

    [USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)服务的功能/设备/外设。 USB 函数控制器类扩展支持 MTP （媒体传输协议），并使用 BC 1.2 充电器进行充电。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供内置的客户端驱动程序。 您可以使用[USB 函数控制器客户端驱动程序编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))编写函数控制器的自定义客户端驱动程序。 有关详细信息，请参阅[开发适用于 USB 功能控制器的 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)。

    SoC 供应商可能会为你提供用于充电器检测的 USB 函数较低筛选器驱动程序。 如果使用的是内置 Synopsys USB 3.0 或 ChipIdea USB 2.0 客户端驱动程序，则可以实现自己的筛选器驱动程序。

-   **USB 主机端驱动程序**

    USB 主机端驱动程序是适用于 EHCI 或 XHCI 兼容 USB 主机控制器的一组驱动程序。 如果角色切换驱动程序枚举主机角色，则会加载驱动程序。 如果主机控制器不符合规范，则可以使用[USB 主机控制器扩展（UCX）编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))编写自定义驱动程序。 有关信息，请参阅[开发适用于 USB 主机控制器的 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)。

    **请注意**  在 Windows 10 移动版上，并非[所有 USB 设备类](supported-usb-classes.md)都受支持。

     

-   **USB 连接器管理器**

    Microsoft 提供了一个带有 Windows （UcmUcsiCx）的 UCSI 内置驱动程序，该驱动程序实现了[此处](https://go.microsoft.com/fwlink/p/?LinkId=703713)提供的 UCSI 规范定义的功能。 该规范介绍了 UCSI 的功能，并说明了硬件组件设计器、系统构建者和设备驱动程序开发人员的寄存器和数据结构。

    此驱动程序适用于具有嵌入式控制器的系统。 此驱动程序是 Microsoft 提供的 USB 连接器管理器类扩展驱动程序（Ucmcx）的客户端。 驱动程序处理任务（例如，启动对固件的请求）以更改数据或电源角色，并获取向用户提供故障排除消息所需的信息。

## <a name="ucsi-commands-required-by-windows"></a>Windows 所需的 UCSI 命令


请参阅所有 UCSI 实现中 "Required" 命令的 UCSI 规范。

除标记为 "必需" 的命令外，Windows 还需要以下命令：

-   获取\_备用\_模式
-   支持\_CAM\_
-   获取\_PDOS
-   将\_通知\_启用：系统或控制器必须支持\_通知通知中的以下通知\_启用：
    -   支持的提供程序功能更改
    -   协商的电源级别更改
-   获取\_连接器\_状态：系统或控制器必须在 GET\_连接器\_状态中支持这些连接器状态更改：
    -   支持的提供程序功能更改
    -   协商的电源级别更改

有关在 BIOS 中实现 UCSI 所需的任务的信息，请参阅[UCSI 的 INTEL BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)。

## <a name="example-flow-for-ucsi"></a>UCSI 的示例流


本部分中给出的示例介绍 USB 类型 C 硬件/固件、UCSI 驱动程序和操作系统之间的交互。

### <a name="drp-role-detection"></a>DRP 角色检测

1.  USB 类型 C 硬件/固件检测到设备附加事件，Windows 10 系统 DRP system 最初成为 UFP 角色。
    1.  该固件发送指示连接器中的更改的通知。
    2.  UCSI 驱动程序\_STATUS 请求发送 GET\_连接器。
    3.  该固件会响应其 Connect Status = 1，连接器 Partner Type = DFP。 
2.  USB 函数堆栈中的驱动程序响应枚举。
3.  USB 连接器管理器类扩展可识别 USB 函数堆栈已加载，因此系统状态错误。 它通知 UCSI 驱动程序发送 "设置 USB 操作" 角色并将 "电源方向" 角色请求设置到固件。
4.  USB 类型 C 硬件/固件用 DFP 启动角色交换操作。

### <a name="detecting-a-charger-mismatch-error--condition"></a>检测充电器不匹配错误情况

1.  USB 类型 C 硬件/固件检测到已连接充电器，并协商默认电源协定。 它还观察到该充电器没有为系统提供足够的电源。
2.  USB 类型 C 硬件/固件设置了充电速度缓慢。
    1.  该固件发送指示连接器中的更改的通知。
    2.  UCSI 驱动程序\_STATUS 请求发送 GET\_连接器。
    3.  固件响应的连接状态 = 1，连接器伙伴类型 = DFP，电池充电状态 = 慢/滴。
    
3.  USB 连接器管理器类扩展将通知发送给 UI，以显示 "充电器不匹配" 消息。

## <a name="how-to-test-ucsi"></a>如何测试 UCSI


有多种方法可以测试 UCSI 实现。 若要测试 UCSI BIOS/EC 实现中的单个命令，请使用[MUTT Software Pack](mutt-software-package.md)中提供的 UCSIControl。 若要测试完整的 UCSI 实现，请使用在 Windows 硬件实验室工具包（HLK）中可以找到的 UCSI 测试以及[类型 C 手动互操作过程](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)中的步骤。

**UCSIControl**

可以使用 UCSIControl 在 UCSI BIOS/EC 实现中测试各个命令。 此工具使你可以通过 UCSI 驱动程序将 UCSI 命令发送到固件。 它要求加载并运行驱动程序，同时还启用了驱动程序的测试接口。 默认情况下，不会启用此界面，因为这样可以防止在零售系统上未经授权的用户对其进行访问。

1.  在设备管理器（devmgmt.msc）中找到名为**UCSI USB 连接器管理器**的设备节点。 节点位于 "**通用串行总线控制器**" 类别下。
2.  右键单击该设备，然后选择 "**属性**" 并打开 "**详细信息**" 选项卡。
3.  从下拉选择 "**设备实例路径**" 并记下属性值。
4.  打开注册表编辑器 (regedit.exe)。
5.  导航到此项下的设备实例路径。

    HKEY\_本地\_计算机\\系统\\CurrentControlSet\\枚举\\&lt;&gt;设备参数\\

6.  创建一个名为**TestInterfaceEnabled**的 DWORD 值，并将其值设置为0x1。
7.  通过选择 "设备管理器中的" 设备 "节点上的"**禁用**"选项，然后选择"**启用**"，重新启动设备。 或者，您可以只重启 PC。

可以通过运行**UcsiControl/？** 来查看帮助。

下面是常用命令：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>UCSI 命令</th>
<th>UcsiControl 命令</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>重置 PPM</td>
<td><strong>UcsiControl 发送 0 1</strong></td>
</tr>
<tr class="even">
<td>连接器重置</td>
<td><p>软重置： <strong>UcsiControl 发送 0 10003</strong></p>
<p>硬重置： <strong>UcsiControl 发送 0 810003</strong></p></td>
</tr>
<tr class="odd">
<td>设置通知启用</td>
<td><p>所有通知： <strong>UcsiControl Send 0 ffff0005</strong></p>
<p>仅命令完成： <strong>UcsiControl Send 0 00010005</strong></p>
<p>无通知： <strong>UcsiControl 发送 0 00000005</strong></p></td>
</tr>
<tr class="even">
<td>获取功能</td>
<td><strong>UcsiControl 发送 0 6</strong></td>
</tr>
<tr class="odd">
<td>获取连接器功能</td>
<td><strong>UcsiControl 发送 0 10007</strong></td>
</tr>
<tr class="even">
<td>设置 UOM</td>
<td><p><strong>DFP： UcsiControl Send 0 810008</strong></p>
<p><strong>UFP： UcsiControl Send 0 1010008</strong></p>
<p><strong>DRP： UcsiControl Send 0 2010008</strong></p></td>
</tr>
<tr class="odd">
<td>设置 UOR</td>
<td><p><strong>DFP： UcsiControl Send 0 810009</strong></p>
<p><strong>UFP： UcsiControl Send 0 1010009</strong></p>
<p><strong>Accept： UcsiControl 发送 0 2010009</strong></p></td>
</tr>
<tr class="even">
<td>设置 PDR</td>
<td><p><strong>提供程序： UcsiControl Send 0 81000B</strong></p>
<p><strong>使用者： UcsiControl Send 0 101000B</strong></p>
<p><strong>Accept： UcsiControl Send 0 201000B</strong></p></td>
</tr>
<tr class="odd">
<td>获取 PDOs</td>
<td><p><strong>本地源： UcsiControl 发送 7 00010010</strong></p>
<p><strong>本地接收器： UcsiControl 发送 3 00010010</strong></p>
<p><strong>远程源： UcsiControl 发送 7 00810010</strong></p>
<p><strong>远程接收器： UcsiControl 发送 3 00810010</strong></p></td>
</tr>
<tr class="even">
<td>获取连接器状态</td>
<td><strong>UcsiControl 发送 0 010012</strong></td>
</tr>
<tr class="odd">
<td>获取错误状态</td>
<td><strong>UcsiControl 发送 0 13</strong></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[体系结构：用于 Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)  



