---
description: 本文提供了有关 Windows 操作系统的 USB ContainerIDs 的信息。 它包含设备制造商对其多功能 USB 设备进行编程以使其能够由 Windows 正确检测的指导原则。
title: Windows 中的 USB ContainerID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c72672db04b21de28fab3e155ed860d305dda3de
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010477"
---
# <a name="usb-containerids-in-windows"></a>Windows 中的 USB ContainerID


本文提供有关 Windows 操作系统的 USB **ContainerID**的信息。 它包含设备制造商对其多功能 USB 设备进行编程以使其能够由 Windows 正确检测的指导原则。

从 Windows 7 开始，用户可以利用连接到其计算机的设备的所有功能。 这包括多功能设备，如打印机、扫描仪和复印机设备的组合。 Windows 7 支持将单个物理设备的所有功能合并到设备容器。 设备容器是物理设备的虚拟表示。 此合并通过将 **ContainerID** 属性分配给为物理设备枚举的每个设备函数来实现。 通过为每个设备函数指定相同的 **ContainerID** 值，Windows 7 将识别出所有设备函数属于同一物理设备。

通过不同总线类型连接到计算机的所有设备类型都可以支持设备容器。 但是，并非所有总线类型都使用相同的机制来生成 **ContainerID**。 对于 USB 设备，设备供应商可以使用 **ContainerID** 描述符来描述物理设备的 **containerid** 。 **ContainerID**描述符是可以存储在 USB 设备固件中的 Microsoft 操作系统功能描述符。 USB 设备制造商必须正确实现其设备中的这些 **ContainerID** 描述符，才能利用 Windows 7 中提供的新设备功能。 无论设备支持多少设备功能，USB 设备制造商都需要为每个物理设备仅实现一个 **ContainerID** 。

有关将单个设备的所有功能合并到设备容器中的详细信息，请参阅 [如何生成容器 id](../install/how-container-ids-are-generated.md)。

有关适用于 USB 设备的 Microsoft OS 描述符的详细信息，请参阅 [MICROSOFT Os 描述符 FOR Usb 设备](microsoft-defined-usb-descriptors.md)。

## <a name="how-a-usb-containerid-is-generated"></a>如何生成 USB ContainerID


以下是为 USB 设备生成 **ContainerID** 的两种方式：

-   USB 设备的制造商通过使用 Microsoft 操作系统**ContainerID**描述符在设备的固件中指定**ContainerID** 。
-   Microsoft USB 集线器驱动程序会自动为设备创建一个 **ContainerID** ，从设备的产品 ID 组合 (PID) 、供应商 ID (VID) 、修订号和序列号。 在这种情况下，Microsoft USB 集线器驱动程序使用最少的功能创建一个 **ContainerID** 。 此方法仅适用于具有唯一序列号的设备。

## <a name="usb-containerid-contents"></a>USB ContainerID 内容


USB **ContainerID** 以全局唯一标识符 (UUID) 字符串形式提供给操作系统。 **Containerid** UUID 包含在**containerid**描述符中。 **ContainerID**描述符是设备级 Microsoft OS 功能描述符。 因此，当操作系统请求使用 USB **ContainerID**时，描述符请求的 wValue 字段必须始终设置为零。 有关 Microsoft 操作系统功能描述符和描述符请求的详细信息，请参阅 [MICROSOFT os 1.0 描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617519)。

**ContainerID**描述符由标头部分组成。

| 偏移量 | 字段          | 大小 | 类型           | 说明                                                                                                                                                                                                                                                                                                                                                                                         |
|--------|----------------|------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0      | **dwLength**   | 4    | 无符号 DWord | 整个 **ContainerID** 说明符的长度（以字节为单位）。 此字段必须始终设置为0x18 值。                                                                                                                                                                                                                                                                                   |
| 4      | **bcdVersion** | 2    | BCD            | 以二进制编码的十进制 (BCD) 中的 **ContainerID** 描述符版本号，其中每个半值对应于一个数字。 最高有效字节 (MSB) 在小数点之前包含两位数，并且最小有效字节 (LSB) 包含小数点后两位数字。 例如，版本1.00 表示为0x0100。 此字段必须始终设置为0x0100。 |
| 6      | **wIndex**     | 2    | 字           | 对于 USB **ContainerID** 描述符，此字段始终设置为6。                                                                                                                                                                                                                                                                                                                                  |

 

**Containerid**描述符包含一个 containerid 部分。

| 偏移量 | 字段            | 大小 | 类型           | 说明           |
|--------|------------------|------|----------------|-----------------------|
| 0      | **bContainerID** | 16   | 无符号 DWord | **ContainerID** 数据。 |

 

设备制造商负责确保设备的每个实例都具有唯一的16字节的 **ContainerID**值。 此外，在每次打开设备时，设备必须报告相同的 **ContainerID** 值。
有多个已建立的用于生成 Uuid 的算法，几乎不会发生重复。 设备制造商可以选择最适合其需求的 UUID 生成算法。 只要结果是唯一的，就可以使用什么 UUID 生成算法，这并不重要。

## <a name="usb-containerid-syntax"></a>USB ContainerID 语法


将使用 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx} 的标准 UUID 字符串格式报告一个 **ContainerID** 。 下面是固件中 0C B4 A7 2C D1 7B 25 4F B5 73 A1 3A 97 5D 的示例表示形式的示例表示 **形式，格式**为 {2CA7B40C-7BD1-4F25-B573-A13A975DDC07} UUID string。

```cpp
UCHAR Example<mark type="member">ContainerID</mark>Descriptor[24] =
{
    0x18, 0x00, 0x00, 0x00,     // dwLength - 24 bytes
    0x00, 0x01,                 // bcdVersion - 1.00
    0x06, 0x00,                 // wIndex – 6 for a <mark type="member">ContainerID</mark>

    0x0C, 0xB4, 0xA7, 0x2C,     // b<mark type="member">ContainerID</mark> -
    0xD1, 0x7B, 0x25, 0x4F,     // {2CA7B40C-7BD1-4F25-B573-A13A975DDC07}
    0xB5, 0x73, 0xA1, 0x3A,     // 0C B4 A7 2C D1 7B 25 4F B5 73 A1 3A 97 5D DC 07
    0x97, 0x5D, 0xDC, 0x07      //
}
```

请注意，在格式化为 UUID 字符串时，前8个字节的字节顺序发生变化。

## <a name="microsoft-os-descriptor-changes"></a>Microsoft OS 描述符更改


为了保留旧的 **ContainerID** 功能，已向 Microsoft OS 字符串描述符添加了一个新的标志字段，该字段可用于指示对 **ContainerID** 描述符的支持。

Microsoft OS 字符串描述符的当前定义包含1个字节的 pad 字段 **bPad**，该字段通常设置为零。 对于支持新 **ContainerID**的 USB 设备， **bPad** 字段将重新定义为标志字段 **bFlags**。 此字段的第1位用于指示对 **ContainerID** 描述符的支持。 表3描述了用于 USB 设备的 Microsoft 操作系统字符串描述符的字段。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>长度 (字节) </th>
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>bLength</strong></td>
<td>1</td>
<td>0x12</td>
<td>描述符的长度。</td>
</tr>
<tr class="even">
<td><strong>bDescriptorType</strong></td>
<td>1</td>
<td>0x03</td>
<td>描述符类型。 值0x03 指示 Microsoft 操作系统字符串描述符。</td>
</tr>
<tr class="odd">
<td><strong>qwSignature</strong></td>
<td>14</td>
<td>'MSFT100'</td>
<td>签名字段。</td>
</tr>
<tr class="even">
<td><strong>bMS_VendorCode</strong></td>
<td>1</td>
<td>供应商代码</td>
<td>供应商代码。</td>
</tr>
<tr class="odd">
<td><strong>bFlags</strong></td>
<td>1</td>
<td>0x02</td>
<td><p>位0：保留</p>
<p>第1位： <strong>ContainerID</strong> 支持</p>
<ul>
<li>0：不支持 <strong>ContainerID</strong></li>
<li>1：支持 <strong>ContainerID</strong></li>
</ul>
<p>Bits 2 –7：保留</p></td>
</tr>
</tbody>
</table>

 

目前，提供支持 Microsoft OS 描述符但不支持 **ContainerID** 描述符的 USB 设备的 **bPad** 字段设置为0x00。 USB 集线器驱动程序不会在此类设备上查询 USB **ContainerID** 说明符。
## <a name="container-view-of-a-usb-multifunction-device"></a>USB 多功能设备的容器视图


**ContainerID**提供了用于整合设备的设备 USB 设备的信息。 图1显示了一个示例，演示如何在产品中的所有单个设备使用同一个 **ContainerID**时，将多功能打印机中的所有设备合并为一个设备容器。

![多功能打印机中的所有设备的合并](images/containerid-multifunction.png)

通过整合多功能 USB 设备的所有设备，可以在 Windows 7 的 "设备和打印机" 中将该物理产品显示为单一设备。 图2显示了在 "设备和打印机" 中显示为单个设备的 USB 多功能键盘和鼠标设备的示例。

![设备和打印机中的多功能设备](images/containerid-multifunction1.png)

## <a name="usb-containerid-hck-requirements"></a>USB ContainerID HCK 要求


设备制造商必须确保它们生成的设备的每个实例都具有全局唯一的 **ContainerID** 值，以便 Windows 能够成功合并每个 USB 多功能设备的功能。 Windows 硬件 CertificationWindows 硬件认证工具包包括一项 DEVFUND-0034，适用于在设备中实现的 USB **ContainerID** 。 如果设备实现 USB **ContainerID**，Windows 硬件认证会将 **Containerid** 测试为 Microsoft OS 描述符测试的一部分，并检查 **containerid** 值是否全局唯一。 有关这些 Windows 硬件认证要求的详细信息，请参阅 Windows 硬件认证网站。

有关实现 USB **ContainerID** 的建议以下是适用于设计、制造和发运 usb 设备的设备供应商的建议：

-   了解 Windows 7 如何通过使用 **ContainerID**来改善对多功能和多个传输 USB 设备的支持。 建议首先阅读 Windows 7 中的 "多功能设备支持和设备容器组合"。
-   请确保每个 USB 设备上的序列号都是唯一的。 Windows 硬件认证要求表明，如果设备包含序列号，则设备的每个实例的序列号都必须是唯一的。
-   不要为嵌入在系统中的 USB 设备提供 **ContainerID** 。 集成 USB 设备应依赖 ACPI BIOS 设置或端口的 USB 集线器描述符 **DeviceRemovable** 位。
-   确保附加到系统的所有 USB 设备都具有唯一的 **ContainerID** 值。 请勿在产品系列之间共享 **ContainerID** 值或 USB 序列号。
-   请确保为设备正确设置可移动设备功能。
    **注意**   将 USB **ContainerID**描述符添加到之前提供的 usb 设备的设备供应商必须在设备的设备描述符中 (**bcdDevice**) 增加设备发布号。 这是必需的，因为 USB 集线器驱动程序会根据设备的供应商 ID、产品 ID 和设备版本号来缓存 Microsoft OS 字符串描述符 (或缺少一个) 。 如果未递增设备版本号，则集线器驱动程序在以前使用同一供应商 ID、产品 ID 和设备发行版（不支持 USB **ContainerID**描述符）枚举设备的实例时，不会查询新设备的 USB **ContainerID** 。

     

## <a name="related-topics"></a>相关主题
[为 Windows 构建 USB 设备](building-usb-devices-for-windows.md)  
[USB 设备的容器 ID](../install/how-usb-devices-are-assigned-container-ids.md)