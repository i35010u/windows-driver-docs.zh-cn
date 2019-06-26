---
title: HID 按钮驱动程序
description: GPIO 按钮; 使用由 Microsoft 提供的按钮驱动程序否则，实现您的驱动程序注入到操作系统的 HID 数据。
ms.assetid: FBA8141D-8DBA-4C68-8BB5-44B3EDB7D062
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da20c3b6476e1ab339e202979d2a6922d4af0e90
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393487"
---
# <a name="hid-button-drivers"></a>HID 按钮驱动程序


**摘要**

-   [描述在 ACPI 和负载由 Microsoft 提供驱动程序中的 GPIO 按钮](acpi-button-device.md)
-   [在非 GPIO 按钮的内核模式下编写 HID 源驱动程序](virtual-hid-framework--vhf-.md)
-   [编写 UMDF HID 微型驱动程序的非 GPIO 按钮](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)

**适用于**

-   Windows 10
-   HID 按钮设备驱动程序开发人员

**重要的 API**

-   [虚拟 HID 框架引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
-   [UMDF HID 微型驱动程序 Ioctl](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))

GPIO 按钮; 使用由 Microsoft 提供的按钮驱动程序否则，实现您的驱动程序注入到操作系统的 HID 数据。

按钮 （电源、 Windows、 卷和旋转锁） 通常用于物理键盘不是可供用户使用，如双用型或平板电脑外形规格上时出现的任务。 按钮声明本身对操作系统为 HID 设备通过提供[HID 按钮报告描述符](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/hid-button-report-descriptors)。 这允许系统来解释的用途和这些按钮的事件的一种标准化方法。 按钮状态发生更改时将该事件映射到[HID 用法](hid-usages.md)。 HID 传输微型驱动程序然后将详细信息发送到 HID 用户模式或内核模式中的客户端的较高级别驱动程序报告这些事件。

为常规用途的物理 I/O (GPIO) 按钮、 HID 传输微型驱动程序是由 Microsoft 提供现成驱动程序基于定义的 GPIO 硬件资源收到的中断事件时进行报告。

现成驱动程序无法服务未绑定到中断行的按钮。 对于此类按钮，您需要自己编写的 HID 类驱动程序 HID 按钮和报告状态更改为公开按钮驱动程序 （提供 Microsoft）。 HID 源驱动程序或 HID 传输驱动程序，可能是您的驱动程序。

## <a name="guidance-for-supporting-hid-buttons"></a>有关支持 HID 按钮指南


以下是一些常规指导来帮助你决定要创建 HID 按钮时应遵循哪一种实现。

![用于实现按钮的决策图](images/button.png)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>使用 Microsoft 提供的框中按钮驱动程序</strong></p>
<p><img src="images/hid-acpi.png" alt="ACPI description of a HID button" /></p></td>
<td><p>如果要实现 GPIO 按钮，描述系统 ACPI 中按钮，以便 Windows 可以加载现成驱动程序，Hidinterrupt.sys，作为事件报告给系统的按钮驱动程序。</p>
<ul>
<li><a href="acpi-button-device.md" data-raw-source="[ACPI button device](acpi-button-device.md)">ACPI 按钮设备</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/button-behavior" data-raw-source="[Button Behavior](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/button-behavior)">按钮行为</a></li>
<li><a href="acpi-button-device.md#acpi-button-phone" data-raw-source="[Sample buttons ACPI for phone/tablet](acpi-button-device.md#acpi-button-phone)">示例按钮 ACPI 手机/平板电脑</a></li>
<li><a href="acpi-button-device.md#acpi-button-desktop" data-raw-source="[Sample buttons ACPI for desktop](acpi-button-device.md#acpi-button-desktop)">示例按钮 ACPI 桌面</a></li>
</ul>
<p>Microsoft 建议你将使用内置传输的微型驱动程序只要有可能。</p></td>
</tr>
<tr class="even">
<td><p><strong>在内核模式下编写 HID 源驱动程序</strong></p>
<p><img src="images/hid-vhf.png" alt="Buttons using Virtual HID Framework" /></p></td>
<td><p>如果需要将其注入由另一个软件组件的 HID 格式中实现如流数据的非 GPIO 按钮，可以选择要写入的内核模式驱动程序。 从 Windows 10 开始，您可以通过调用通信与虚拟 HID Framework (VHF) 和获取和设置隐藏报表与 HID 类驱动程序的编程接口编写 HID 源驱动程序。</p>
<ul>
<li><a href="virtual-hid-framework--vhf-.md" data-raw-source="[How to write a HID source driver that interacts with Virtual HID Framework (VHF)](virtual-hid-framework--vhf-.md)">如何编写使用虚拟 HID Framework (VHF) 进行交互的 HID 源驱动程序</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index" data-raw-source="[Virtual HID Framework Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)">虚拟 HID 框架引用</a></li>
</ul>
<p>或者，可以编写所支持的早期版本的 Windows 内核模式 HID 传输微型驱动程序。 但是，我们不建议此方法因为编写质量差的 KMDF HID 传输微型驱动程序可以使系统崩溃。</p>
<ul>
<li><a href="transport-minidrivers.md" data-raw-source="[Transport Minidrivers](transport-minidrivers.md)">传输微型驱动程序</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index" data-raw-source="[HID Minidriver IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)">HID 微型驱动程序 Ioctl</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>编写 UMDF HID 微型驱动程序</strong></p>
<p><img src="images/hid-umdf.png" alt="HID Transport Minidriver" /></p></td>
<td><p>如果要实现非 GPIO 按钮，而不是使用上述模型编写的 HID 源驱动程序，您可以在用户模式下编写 HID 传输微型驱动程序。 这些驱动程序更轻松地与内核模式驱动程序开发中，此驱动程序中的错误进行不 bug 检查整个系统。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers" data-raw-source="[Creating UMDF HID Minidrivers](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)">创建 UMDF HID 微型驱动程序</a></li>
<li><a href="https://docs.microsoft.com/previous-versions/hh463977(v=vs.85)" data-raw-source="[UMDF HID Minidriver IOCTLs](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))">UMDF HID 微型驱动程序 Ioctl</a></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="universal-windows-drivers-for-hid-buttons"></a>HID 按钮的通用 Windows 驱动程序


从 Windows 10 开始，HID 驱动程序的编程接口是基于 OneCoreUAP 的 Windows 版本的一部分。 通过使用此组通用的接口，您可以编写通过使用按钮驱动程序[虚拟 HID 框架](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)或[传输微型驱动程序](transport-minidrivers.md)接口。 这些驱动程序将运行上同时面向桌面版本中 （主页、 专业版、 企业版和教育版） 的 Windows 10 和 Windows 10 移动版，以及其他 Windows 10 版本。

有关分步指南，请参阅[通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers)。

## <a name="related-topics"></a>相关主题
[人机接口设备](https://developer.microsoft.com/windows/hardware)  



