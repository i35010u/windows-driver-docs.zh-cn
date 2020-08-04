---
Description: Microsoft 提供与 USB 类型 C 连接器系统软件接口 (UCSI) 规范兼容的驱动程序。
title: USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: d2301377daf1057a90220785404b459182499f86
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402270"
---
# <a name="usb-type-c-connector-system-software-interface-ucsi-driver"></a>USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序


**摘要**

-   Microsoft 提供的随机 UCSI 驱动程序，适用于带有嵌入式控制器的 USB 类型 C 系统。

**上次更新时间**

-   2018 年 10 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

**官方规范**

-   [UCSI 的 Intel BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 类型 C 连接器系统软件接口规范](https://go.microsoft.com/fwlink/p/?LinkId=703713)
-   [硬件设计：适用于带有嵌入式控制器的系统的 USB 类型 C 组件](hardware-design-of-a-usb-type-c-system.md#emb)


Microsoft 为 ACPI 传输提供与 USB 类型 C 连接器系统软件接口 (UCSI) 规范兼容的驱动程序。 如果你的设计包含带有 ACPI 传输的嵌入式控制器，请在系统的 BIOS/EC 中实现 UCSI，并加载随机 UCSI 驱动程序（UcmUcsiCx.sys 和 UcmUcsiAcpiClient.sys）。

如果与 UCSI 兼容的硬件使用的是非 ACPI 传输，则需要[写入 UCSI 客户端驱动程序](write-a-ucsi-driver.md)。

## <a name="drivers-for-supporting-usb-type-c-components-for-systems-with-embedded-controllers"></a>用于支持带嵌入式控制器的系统的 USB 类型 C 组件的驱动程序

下面是具有嵌入式控制器的系统的示例。

![USB 类型 C 软件组件](images/ucsiarch.png)

在前面的示例中，USB 角色切换在系统的固件中进行处理，并且未加载 USB 角色切换驱动程序堆栈。 在另一个系统中，可能无法加载驱动程序堆栈，因为不支持双重角色。

在上图中，

-   **USB 设备端驱动程序**

    [USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)为功能/设备/外设提供服务。 USB 功能控制器类扩展支持 MTP（媒体传输协议），并使用 BC 1.2 充电器进行充电。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供随机客户端驱动程序。 可以通过使用 [USB 功能控制器客户端驱动程序编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))，为功能控制器编写自定义客户端驱动程序。 有关详细信息，请参阅[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)。

    SoC 供应商可能会为你提供用于进行充电器检测的 USB 功能下层筛选器驱动程序。 如果使用的是随机 Synopsys USB 3.0 或 ChipIdea USB 2.0 客户端驱动程序，则可以实现自己的筛选器驱动程序。

-   **USB 主机端驱动程序**

    USB 主机端驱动程序是适用于与 EHCI 或 XHCI 兼容的 USB 主机控制器的一组驱动程序。 如果角色切换驱动程序枚举主机角色，则会加载驱动程序。 如果主机控制器不符合规范，则可以使用 [USB 主机控制器扩展 (UCX) 编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))来写入自定义驱动程序。 有关信息，请参阅[为 USB 主机控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)。

    请注意，    并非[所有 USB 设备类](supported-usb-classes.md)在 Windows 10 移动版上都受支持。

     

-   **USB 连接器管理器**

    Microsoft 提供带有 Windows (UcmUcsiCx.sys) 的 UCSI 随机驱动程序，它实现了在 [USB Type-C 连接器系统软件接口规范](https://go.microsoft.com/fwlink/p/?LinkId=703713)中定义的功能。 该规范介绍了 UCSI 的功能，并说明了硬件组件设计师、系统组装商和设备驱动程序开发人员的寄存器和数据结构。

    此驱动程序适用于具有嵌入式控制器的系统。 此驱动程序是 Microsoft 提供的 USB 连接器管理器类扩展驱动程序 (Ucmcx.sys) 的客户端。 驱动程序处理任务（例如，启动对固件的请求）以更改数据或电源角色，并获取向用户提供故障排除消息所需的信息。

## <a name="ucsi-commands-required-by-windows"></a>Windows 所需的 UCSI 命令


请参阅所有 UCSI 实现中“必需”命令的 UCSI 规范。

除标记为“必需”的命令外，Windows 还需要以下命令：

-   GET\_ALTERNATE\_MODES
-   GET\_CAM\_SUPPORTED
-   GET\_PDOS
-   SET\_NOTIFICATION\_ENABLE：系统或控制器在 SET\_NOTIFICATION\_ENABLE 中必须支持下列通知：
    -   支持的提供程序功能更改
    -   协商的电源级别更改
-   GET\_CONNECTOR\_STATUS：系统或控制器在 GET\_CONNECTOR\_STATUS 中必须支持下列连接器状态更改：
    -   支持的提供程序功能更改
    -   协商的电源级别更改

有关在 BIOS 中实现 UCSI 所需的任务的信息，请参阅 [UCSI 的 Intel BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)。

## <a name="example-flow-for-ucsi"></a>UCSI 的示例流


本部分中给出的示例描述了 USB 类型 C 硬件/固件、UCSI 驱动程序和操作系统之间的交互。

### <a name="drp-role-detection"></a>DRP 角色检测

1.  USB 类型 C 硬件/固件检测到设备附加事件，Windows 10 系统 DRP 系统最初成为 UFP 角色。
    1.  该固件发送指示连接器中的更改的通知。
    2.  UCSI 驱动程序发送 GET\_CONNECTOR\_STATUS 请求。
    3.  该固件会响应其 Connect Status = 1，Connector Partner Type = DFP。 
2.  USB 功能堆栈中的驱动程序响应枚举。
3.  USB 连接器管理器类扩展可识别 USB 功能堆栈已加载，因此系统处于错误状态。 它通知 UCSI 驱动程序向固件发送“设置 USB 操作角色”和“设置电源方向角色”请求。
4.  USB 类型 C 硬件/固件用 DFP 启动角色交换操作。

### <a name="detecting-a-charger-mismatch-error-condition"></a><a name="detecting-a-charger-mismatch-error--condition"></a>检测充电器不匹配错误情况

1.  USB 类型 C 硬件/固件检测到已连接充电器，并协商默认电源协定。 它还观察到该充电器没有为系统提供足够的电源。
2.  USB 类型 C 硬件/固件设置了缓慢充电速度。
    1.  该固件发送指示连接器中的更改的通知。
    2.  UCSI 驱动程序发送 GET\_CONNECTOR\_STATUS 请求。
    3.  固件响应为 Connect Status = 1，Connector Partner Type=DFP 和 Battery Charging Status = Slow/Trickle。
    
3.  USB 连接器管理器类扩展向 UI 发送通知，以显示充电器不匹配故障排除消息。

## <a name="how-to-test-ucsi"></a>如何测试 UCSI


有多种方法可以测试 UCSI 实现。 要测试 UCSI BIOS/EC 实现中的单个命令，请使用 [MUTT 软件包](mutt-software-package.md)中提供的 UCSIControl.exe。 要测试完整的 UCSI 实现，请使用 Windows Hardware Lab Kit (HLK) 中可找到的 UCSI 测试，以及[类型 C 手动互操作过程](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)中的步骤。

**UCSIControl.exe**

可以使用 UCSIControl.exe 在 UCSI BIOS/EC 实现中测试各个命令。 此工具使你可以通过 UCSI 驱动程序将 UCSI 命令发送到固件。 它要求加载并运行驱动程序，同时还启用了驱动程序的测试接口。 默认情况下，不会启用此界面，因为这样可以防止在零售系统上未经授权的用户对其进行访问。

1.  在设备管理器 (devmgmt.msc) 中找到名为“UCSI USB 连接器管理器”  的设备节点。 节点位于“通用串行总线控制器”  类别下。
2.  右键单击该设备，然后选择“属性”  并打开“详细信息”  选项卡。
3.  从下拉列表中选择“设备实例路径”  ，并记下属性值。
4.  打开注册表编辑器 (regedit.exe)。
5.  导航到此项下的设备实例路径。

    HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Enum\\&lt;device-instance-path&gt;\\Device Parameters

6.  创建一个名为“TestInterfaceEnabled”  的 DWORD 值，并将该值设置为 0x1。
7.  通过在“设备管理器”中的设备节点上选择“禁用”  选项，然后选择“启用”  来重启设备。 或者，可以只重启电脑。

可以通过运行 UcsiControl.exe /?  查看帮助。

下面是常用命令：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>UCSI 命令</th>
<th>UcsiControl.exe 命令</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PPM Reset</td>
<td>UcsiControl.exe Send 0 1</td>
</tr>
<tr class="even">
<td>Connector Reset</td>
<td><p>软重置：UcsiControl.exe Send 0 10003</p>
<p>硬重置：UcsiControl.exe Send 0 810003</p></td>
</tr>
<tr class="odd">
<td>Set Notification Enable</td>
<td><p>所有通知：UcsiControl.exe Send 0 ffff0005</p>
<p>仅命令完成：UcsiControl.exe Send 0 00010005</p>
<p>无通知：UcsiControl.exe Send 0 00000005</p></td>
</tr>
<tr class="even">
<td>Get Capability</td>
<td>UcsiControl.exe Send 0 6</td>
</tr>
<tr class="odd">
<td>Get Connector Capability</td>
<td>UcsiControl.exe Send 0 10007</td>
</tr>
<tr class="even">
<td>Set UOM</td>
<td><p>DFP：UcsiControl.exe Send 0 810008</p>
<p>UFP：UcsiControl.exe Send 0 1010008</p>
<p>DRP：UcsiControl.exe Send 0 2010008</p></td>
</tr>
<tr class="odd">
<td>Set UOR</td>
<td><p>DFP：UcsiControl.exe Send 0 810009</p>
<p>UFP：UcsiControl.exe Send 0 1010009</p>
<p>接受：UcsiControl.exe Send 0 2010009</p></td>
</tr>
<tr class="even">
<td>Set PDR</td>
<td><p>提供方：UcsiControl.exe Send 0 81000B</p>
<p>使用者：UcsiControl.exe Send 0 101000B</p>
<p>接受：UcsiControl.exe Send 0 201000B</p></td>
</tr>
<tr class="odd">
<td>Get PDOs</td>
<td><p>本地源：UcsiControl.exe Send 7 00010010</p>
<p>本地接收器：UcsiControl.exe Send 3 00010010</p>
<p>远程源：UcsiControl.exe Send 7 00810010</p>
<p>远程接收器：UcsiControl.exe Send 3 00810010</p></td>
</tr>
<tr class="even">
<td>Get Connector Status</td>
<td>UcsiControl.exe Send 0 010012</td>
</tr>
<tr class="odd">
<td>Get Error Status</td>
<td>UcsiControl.exe Send 0 13</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[体系结构：Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)  



