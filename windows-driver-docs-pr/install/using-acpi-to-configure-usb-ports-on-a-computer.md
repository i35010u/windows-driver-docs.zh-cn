---
title: 使用 ACPI 配置计算机上的 USB 端口
description: 使用 ACPI 配置计算机上的 USB 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c39c9a37d86343bb6eb5163ce48aa65b0855241
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805445"
---
# <a name="using-acpi-to-configure-usb-ports-on-a-computer"></a>使用 ACPI 配置计算机上的 USB 端口


如果系统需要更改 ACPI BIOS 才能准确反映 USB 端口配置，则你应考虑在配置端口时用户将设备连接到端口。

如果使用 ACPI 来指定 USB 端口的配置，则必须 (**_UPC**) 和物理位置描述 (**_PLD**) 对象中定义 usb 端口功能。 尽管 ACPI 6.0 规范并不明确禁止只使用 **_UPC** 对象，但同时使用这两个对象会更精确地指示用户将设备连接到端口的能力。 仅使用 **_UPC** 对象可能不会正确或按预期设置设备容器分组。

如果设置了 **DeviceRemovable** 位，则连接到该端口的设备将从中心可移动。 下表显示给定端口的 ACPI 对象的值如何影响 Windows 为设备报告的 USB 集线器描述符 **DeviceRemovable** 位的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 端口状态</th>
<th align="left">示例</th>
<th align="left">_UPC。PortIsConnectable 字节</th>
<th align="left">_PLD。UserVisible 位 (位 64) </th>
<th align="left">生成的 DeviceRemovable 位值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>端口可见，用户可以自由连接和断开设备连接。</p></td>
<td align="left"><p>端口在计算机上可供用户查看的面板表面上公开。</p></td>
<td align="left"><p>设置 (0xFF) </p></td>
<td align="left"><p>设置 (1) </p></td>
<td align="left"><p>设置</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口处于隐藏或内部，用户无法自由连接和断开设备连接。</p></td>
<td align="left"><p>端口直接硬连接到集成设备，如便携式计算机网络摄像机或内部 USB 集线器。</p></td>
<td align="left"><p>设置 (0xFF) </p></td>
<td align="left"><p>已清除</p></td>
<td align="left"><p>已清除</p></td>
</tr>
<tr class="odd">
<td align="left"><p>端口由 USB 主机控制器物理实现，但未使用。</p></td>
<td align="left"><p>端口是未连接到端口插头终端或集成设备的多余端口。</p></td>
<td align="left"><p>已清除 (0x00) </p></td>
<td align="left"><p>清除</p></td>
<td align="left"><p>已清除</p></td>
</tr>
</tbody>
</table>

 

**注意**   此配置无效，无法将端口定义为不可连接，但对用户可见。

 

以下示例显示了正确的格式 ACPI 源语言 (ASL) ，它演示了如何使用 **_UPC** 和 **_PLD** 对象来描述 USB 端口：

-   若要指定内部 (用户不可见的端口) 并且可以连接到集成设备， **_UPC。PortIsConnectable** 字节必须设置为0xff 和 **_PLD。UserVisible** 位必须设置为0。

    在以下示例中，设备与计算机的设备容器组合在一起。

    ```cpp
    Name(_UPC, Package(){
        0xFF,         // Port is connectable
        0xFF,         // Connector type (N/A for non-visible ports)
        0x00000000,   // Reserved 0, must be zero
        0x00000000})  // Reserved 1, must be zero

    Name(_PLD, Buffer(0x10){
        0x81, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x30, 0x1C, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00})
    ```

-   若要指定外部的端口 (用户可见) 并且可以连接到外部设备， **_UPC。PortIsConnectable** 字节必须设置为0xff 和 **_PLD。UserVisible** 位必须设置为1。 _ **UPC**。**PortConnectorType** byte 必须设置为 ACPI 3.0 规范第9.13 节中指定的相应 USB 连接器类型。

    在以下示例中，为设备分配了新的设备容器，并显示为单独的物理设备。

    ```cpp
    Name(_UPC, Package(){
        0xFF,         // Port is connectable
        0x00,         // Connector type, Type 'A' in this case
        0x00000000,   // Reserved 0, must be zero
        0x00000000})  // Reserved 1, must be zero

    Name(_PLD, Buffer(0x10){
        0x81, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x31, 0x1C, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00})
    ```
    
为了传递 [Usb 类型 c Acpi 验证](/windows-hardware/test/hlk/testref/b3c41a3f-b844-4c2d-b115-dad51a37f123) 硬件实验室工具包测试，必须在 ACPI 中正确描述 Usb 类型 c 连接器。

USB 类型 C 连接器的示例 _UPC：
```cpp
      Name(_UPC, Package(4){
        0x01,                       // Port is connectable
        0x09,                       // Connector type: Type C connector - USB2 and SS with Switch
        0x00000000,                 // Reserved0 – must be zero
        0x00000000})                // Reserved1 – must be zero
```

有关 ACPI 6.0 接口的详细信息，请参阅 [高级配置和电源接口规范修订版本 6.0](https://go.microsoft.com/fwlink/?LinkId=827852)。

 

