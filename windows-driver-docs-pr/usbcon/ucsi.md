---
Description: Microsoft 提供了符合 USB 类型 C 连接器系统软件接口 (UCSI) 规范的驱动程序。
title: USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be6ee091146807d11c417b80c4f6645702eac6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368786"
---
# <a name="usb-type-c-connector-system-software-interface-ucsi-driver"></a>USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序


**摘要**

-   Microsoft 提供现成 UCSI 驱动程序与嵌入式控制器 USB C 类型系统。

**上次更新时间**

-   2018 年 10 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

**正式规范**

-   [UCSI Intel BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 类型 C 连接器系统软件接口规范](https://go.microsoft.com/fwlink/p/?LinkId=703713)
-   [硬件设计：对于使用嵌入控制器的系统的 USB 类型 C 组件](hardware-design-of-a-usb-type-c-system.md#emb)


Microsoft 为 ACPI 传输提供符合 USB 类型 C 连接器系统软件接口 (UCSI) 规范的驱动程序。 如果您的设计包括 ACPI 传输与嵌入式的控制器，在您的系统 BIOS/EC 中实现 UCSI 和加载现成 UCSI 驱动程序 （UcmUcsiCx.sys 和 UcmUcsiAcpiClient.sys）。

如果你符合 UCSI 的硬件使用非 ACPI 的传输，则需要[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)。

## <a name="drivers-for-supporting-usb-type-c-components-for-systems-with-embedded-controllers"></a>对于使用嵌入控制器的系统支持 USB 类型 C 组件的驱动程序

下面是系统的具有嵌入式控制器的示例。

![usb 类型 c 软件组件](images/ucsiarch.png)

在前面的示例中，USB 角色切换的系统固件中处理和 USB 角色切换驱动程序堆栈不会加载。 在另一个系统中，驱动程序堆栈可能没有获取加载，因为不支持双角色。

在上图中，

-   **USB 设备端驱动程序**

    [USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)服务函数/设备/外设。 USB 函数控制器类扩展支持 MTP （媒体传输协议） 和充电使用 BC 1.2 充电器。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供内置客户端驱动程序。 你可以通过使用为函数控制器编写自定义客户端驱动程序[USB 函数控制器客户端驱动程序的编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))。 有关详细信息，请参阅[开发的 Windows USB 驱动程序函数控制器](developing-windows-drivers-for-usb-function-controllers.md)。

    SoC 供应商可能会为您提供 USB 函数较低筛选器驱动程序的充电器检测。 如果您使用现成 Synopsys USB 3.0 或 ChipIdea USB 2.0 客户端驱动程序，则可以实现你自己的筛选器驱动程序。

-   **USB 宿主端驱动程序**

    USB 宿主端驱动程序是一组使用 EHCI 或 XHCI 符合 USB 主控制器的驱动程序。 如果在角色切换驱动程序枚举主机角色，将加载的驱动程序。 如果您的主控制器不符合规范，则可以通过编写自定义驱动程序[USB 主机控制器扩展 (UCX) 编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))。 有关信息，请参阅[开发的 Windows USB 驱动程序托管控制器](developing-windows-drivers-for-usb-host-controllers.md)。

    **请注意**  不[USB 设备的所有类](supported-usb-classes.md)在 Windows 10 移动版上受支持。

     

-   **USB 连接器管理器**

    Microsoft 提供 UCSI 现成驱动程序与 Windows (UcmUcsiCx.sys) 实现可用 UCSI 规范所定义的功能[此处](https://go.microsoft.com/fwlink/p/?LinkId=703713)。 介绍 UCSI 的功能和硬件组件设计人员、 系统构建者和设备驱动程序开发人员说明的寄存器和数据结构的规范。

    此驱动程序适用于具有嵌入式控制器的系统。 此驱动程序是由 Microsoft 提供的 USB 连接器管理器类扩展驱动程序 (Ucmcx.sys) 的客户端。 该驱动程序处理任务，例如启动对固件更改数据或电源角色的请求和获取故障排除消息提供给用户所需的信息。

## <a name="ucsi-commands-required-by-windows"></a>所必需的 Windows UCSI 命令


请参阅命令"中需要的"所有 UCSI 实现 UCSI 规范。

除了标记为"必需"的命令，Windows 还需要这些命令：

-   GET\_ALTERNATE\_MODES
-   获取\_CAM\_支持
-   获取\_PDOS
-   设置\_通知\_启用：系统或控制器必须支持以下通知集内的\_通知\_启用：
    -   支持的提供程序功能更改
    -   协商的功率级别更改
-   获取\_连接器\_状态：系统或控制器必须支持这些连接器状态更改中获取\_连接器\_状态：
    -   支持的提供程序功能更改
    -   协商的功率级别更改

有关在 BIOS 中实现 UCSI 所需的任务的信息，请参阅[Intel BIOS UCSI 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)。

## <a name="example-flow-for-ucsi"></a>有关 UCSI 流示例


此节中给出的示例描述 USB 类型 C 硬件/固件、 UCSI 驱动程序和操作系统之间的交互。

### <a name="drp-role-detection"></a>DRP 角色检测

1.  USB 类型 C 硬件/固件检测到设备附加事件和 Windows 10 系统 DRP 系统最初将成为 UFP 角色。
    1.  固件将发送一个通知，指示连接器中的更改。
    2.  UCSI 驱动程序将发送 GET\_连接器\_状态请求。
    3.  固件响应其连接状态 = 1 且连接器合作伙伴类型 = DFP。 
2.  USB 函数堆栈中的驱动程序响应的枚举。
3.  USB 连接器管理器类扩展识别出 USB 函数堆栈已加载系统因此处于错误状态。 它指示 UCSI 驱动程序将设置 USB 操作角色和设置电源方向角色请求发送到固件。
4.  USB 类型 C 硬件/固件启动与 DFP 角色交换操作。

### <a name="detecting-a-charger-mismatch-error--condition"></a>检测到充电器不匹配错误情况

1.  USB 类型 C 硬件/固件检测到充电器连接并协商的默认电源协定。 它还将观察充电器没有提供足够系统电源。
2.  USB 类型 C 硬件/固件设置慢速充电位。
    1.  固件将发送一个通知，指示连接器中的更改。
    2.  UCSI 驱动程序将发送 GET\_连接器\_状态请求。
    3.  固件进行响应，连接状态 = 1，连接器合作伙伴类型 = DFP 和电池充电状态 = 慢/滴送。
    
3.  USB 连接器管理器类扩展将通知发送到 UI 来显示充电器不匹配对消息进行故障排除。

## <a name="how-to-test-ucsi"></a>如何测试 UCSI


有多种方法来测试 UCSI 实现。 若要测试单个命令在 UCSI BIOS/EC 实现中，使用 UCSIControl.exe 中, 提供[MUTT 软件 Pack](mutt-software-package.md)。 若要测试完整的 UCSI 实现，使用这两个 UCSI 测试可以在 Windows 硬件 Lab Kit (HLK) 和中的步骤中找到[互操作的类型-C 手动过程](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)。

**UCSIControl.exe**

可以通过使用 UCSIControl.exe UCSI BIOS/EC 实现中测试单个命令。 此工具，可将 UCSI 命令发送到通过 UCSI 驱动程序的固件。 它需要驱动程序加载和运行，并且还具有已启用驱动程序的测试接口。 默认情况下，以防止其被未经授权的零售系统上的用户可以访问未启用此接口。

1.  查找在设备管理器 (devmgmt.msc) 名为设备节点**UCSI USB 连接器管理器**。 该节点是下**通用串行总线控制器**类别。
2.  在设备上，右键单击并选择**属性**，然后打开**详细信息**选项卡。
3.  选择**设备实例路径**从下拉列表并记下属性值。
4.  打开注册表编辑器 (regedit.exe)。
5.  导航到此项下的设备实例路径。

    HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Enum\\&lt;device-instance-path&gt;\\Device Parameters

6.  创建一个名为**TestInterfaceEnabled**并将值设置为 0x1。
7.  通过选择重启设备**禁用**选项在设备管理器中，在设备节点上，然后选择**启用**。 或者，您可以只需重新启动 PC。

可以通过运行查看的帮助**UcsiControl.exe /？** 。

下面是常用的命令：

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
<td>PPM 重置</td>
<td><strong>UcsiControl.exe 发送 0 1</strong></td>
</tr>
<tr class="even">
<td>连接器重置</td>
<td><p>软重置：<strong>UcsiControl.exe Send 0 10003</strong></p>
<p>硬重置：<strong>UcsiControl.exe Send 0 810003</strong></p></td>
</tr>
<tr class="odd">
<td>设置通知</td>
<td><p>所有通知：<strong>UcsiControl.exe Send 0 ffff0005</strong></p>
<p>仅命令完成：<strong>UcsiControl.exe Send 0 00010005</strong></p>
<p>不显示通知：<strong>UcsiControl.exe Send 0 00000005</strong></p></td>
</tr>
<tr class="even">
<td>获取功能</td>
<td><strong>UcsiControl.exe 发送 0 6</strong></td>
</tr>
<tr class="odd">
<td>获取连接器功能</td>
<td><strong>UcsiControl.exe Send 0 10007</strong></td>
</tr>
<tr class="even">
<td>设置 UOM</td>
<td><p><strong>DFP:UcsiControl.exe Send 0 810008</strong></p>
<p><strong>UFP:UcsiControl.exe Send 0 1010008</strong></p>
<p><strong>DRP:UcsiControl.exe Send 0 2010008</strong></p></td>
</tr>
<tr class="odd">
<td>设置 UOR</td>
<td><p><strong>DFP:UcsiControl.exe Send 0 810009</strong></p>
<p><strong>UFP:UcsiControl.exe Send 0 1010009</strong></p>
<p><strong>接受：UcsiControl.exe Send 0 2010009</strong></p></td>
</tr>
<tr class="even">
<td>设置人民民主共和国</td>
<td><p><strong>提供程序：UcsiControl.exe Send 0 81000B</strong></p>
<p><strong>使用者：UcsiControl.exe Send 0 101000B</strong></p>
<p><strong>接受：UcsiControl.exe Send 0 201000B</strong></p></td>
</tr>
<tr class="odd">
<td>获取 PDOs</td>
<td><p><strong>本地源：UcsiControl.exe Send 7 00010010</strong></p>
<p><strong>本地接收器：UcsiControl.exe Send 3 00010010</strong></p>
<p><strong>远程源：UcsiControl.exe Send 7 00810010</strong></p>
<p><strong>远程接收器：UcsiControl.exe Send 3 00810010</strong></p></td>
</tr>
<tr class="even">
<td>获取连接器状态</td>
<td><strong>UcsiControl.exe Send 0 010012</strong></td>
</tr>
<tr class="odd">
<td>获取错误状态</td>
<td><strong>UcsiControl.exe 发送 0 13</strong></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[体系结构：Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)  



