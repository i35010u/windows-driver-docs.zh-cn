---
title: 使用 ACPI 配置计算机上的 USB 端口
description: 使用 ACPI 配置计算机上的 USB 端口
ms.assetid: 999f9fef-512c-415a-abc6-d64560c5c2f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1eaaee115eb76b3652dd335ecff7d56145bdbeb
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349302"
---
# <a name="using-acpi-to-configure-usb-ports-on-a-computer"></a>使用 ACPI 配置计算机上的 USB 端口


如果系统需要 ACPI BIOS 更改，以准确地反映 USB 端口配置，则应考虑用户的功能配置端口时，将设备连接到的端口。

如果您使用 ACPI 指定 USB 端口的配置，则必须定义的 USB 端口功能 (**_UPC**) 和物理位置说明 (**_PLD**) 对象。 尽管 ACPI 6.0 规范不明确禁止使用唯一 **_UPC**对象，这两个对象更多使用精确地指示用户能够将设备连接到端口。 仅使用 **_UPC**对象可能未设置正确，或按预期方式分组的设备容器。

连接到端口的设备是从中心可移动如果**DeviceRemovable**位设置。 下表显示了给定的端口的 ACPI 对象的值如何影响 USB 集线器描述符的值**DeviceRemovable** Windows 报告的设备的位。

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
<th align="left">_PLD。UserVisible 位 （64 位）</th>
<th align="left">生成的 DeviceRemovable 位值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>端口是可见，用户可以自由地连接和断开设备。</p></td>
<td align="left"><p>是对用户可见的计算机上的面板的表面上公开端口。</p></td>
<td align="left"><p>设置 (0xFF)</p></td>
<td align="left"><p>设置 (1)</p></td>
<td align="left"><p>设置</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口是隐藏的或内部，用户不能自由地连接和断开设备。</p></td>
<td align="left"><p>端口是直接硬连线到集成的设备，如便携式计算机网络摄像头或内部的 USB 集线器。</p></td>
<td align="left"><p>设置 (0xFF)</p></td>
<td align="left"><p>清除</p></td>
<td align="left"><p>清除</p></td>
</tr>
<tr class="odd">
<td align="left"><p>端口以物理方式实现通过 USB 主控制器，但不是使用。</p></td>
<td align="left"><p>端口是未连接到端口即插即用终端或集成的设备过多端口。</p></td>
<td align="left"><p>已清除 (0x00)</p></td>
<td align="left"><p>Clear</p></td>
<td align="left"><p>清除</p></td>
</tr>
</tbody>
</table>

 

**请注意**  它是无效的配置将定义为不可连接，但对用户可见的一个端口。

 

下面的示例演示正确 ACPI 源语言 (ASL)，演示如何使用 **_UPC**并 **_PLD**对象来描述的 USB 端口：

-   若要指定是内部端口 （对用户不可见），并可以连接到一个集成的设备， **_UPC。PortIsConnectable**字节必须设置为 0xFF 和 **_PLD。UserVisible**位必须设置为 0。

    在下面的示例设备与计算机的设备容器进行分组。

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

-   若要指定外部端口 （用户可见），并可以连接到外部设备， **_UPC。PortIsConnectable**字节必须设置为 0xFF 和 **_PLD。UserVisible**位必须设置为 1。 _**UPC**。**PortConnectorType**字节必须作为的 ACPI 3.0 规范中的指定部分 9.13 才能设置为适当的 USB 连接器类型。

    在下面的示例设备分配一个新的设备容器，并显示为一个单独的物理设备。

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
    
USB 类型 C 连接器必须正确中所述 ACPI 才能通过[USB 类型 C ACPI 验证](https://msdn.microsoft.com/library/windows/hardware/mt770585(v=vs.85).aspx)硬件实验室工具包测试。

示例 _UPC USB 类型 C 连接器：
```cpp
      Name(_UPC, Package(4){
        0x01,                       // Port is connectable
        0x09,                       // Connector type: Type C connector - USB2 and SS with Switch
        0x00000000,                 // Reserved0 – must be zero
        0x00000000})                // Reserved1 – must be zero
```

ACPI 6.0 接口的详细信息，请参阅[高级配置和电源接口规范 Revision 6.0](https://go.microsoft.com/fwlink/?LinkId=827852)。

 

 





