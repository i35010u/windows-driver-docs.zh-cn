---
Description: This paper provides information about USB ContainerIDs for the Windows operating system. It includes guidelines for device manufacturers to program their multifunction USB devices so that they can be correctly detected by Windows.
title: Windows 中的 USB ContainerID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8214980cf6f42494b66141d8791922955aee635
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567716"
---
# <a name="usb-containerids-in-windows"></a>Windows 中的 USB ContainerID


本白皮书介绍有关 USB **ContainerID**的 Windows 操作系统。 它包括进行编程，以便它们可以正确检测 Windows 其多功能的 USB 设备的设备制造商的指导原则。

从 Windows 7 开始，用户可以充分利用连接到他们的计算机的设备的所有功能。 这包括多功能设备，如组合打印机、 扫描仪和复制器设备。 Windows 7 包括对合并的所有功能在单个物理设备到设备容器的支持。 设备容器是物理设备的虚拟表示。 通过分配来实现这种整合**ContainerID**属性设置为物理设备枚举每个设备函数。 通过分配相同**ContainerID**到每个设备函数，Windows 7 的值可以识别设备的所有函数都属于同一个物理设备。

所有类型的设备连接到通过其他总线类型的计算机可以都支持的设备容器。 但是，并非所有的总线类型使用相同的机制来生成**ContainerID**。 对于 USB 设备，设备供应商可以使用**ContainerID**描述符来描述**ContainerID** 。 对于物理设备。 一个**ContainerID**描述符是可以存储在 USB 设备的固件的 Microsoft 操作系统功能描述符。 USB 设备制造商必须正确实现这些**ContainerID**在其设备，以便充分利用 Windows 7 中提供的新设备功能的描述符。 USB 设备制造商需要实现只有一个**ContainerID**为每个物理设备，而不考虑设备支持多少设备函数。

有关合并的所有功能的单个设备的设备容器到详细信息，请参阅[生成如何容器 Id](https://msdn.microsoft.com/library/windows/hardware/ff546193)。

有关 Microsoft 操作系统描述符的 USB 设备的详细信息，请参阅[USB 设备的 Microsoft 操作系统描述符](microsoft-defined-usb-descriptors.md)。

## <a name="how-a-usb-containerid-is-generated"></a>如何生成 USB ContainerID


以下是两种方法来生成**ContainerID** USB 设备：

-   指定的 USB 设备制造商**ContainerID**中通过使用 Microsoft 操作系统的设备的固件**ContainerID**描述符。
-   Microsoft USB 集线器驱动程序会自动创建**ContainerID**从设备的产品 ID (PID) 的组合、 供应商 ID (VID)、 修订号和序列号的设备。 在这种情况下，Microsoft USB 集线器驱动程序将创建**ContainerID**具有最小功能。 此方法仅适用于具有唯一的序列号的设备。

## <a name="usb-containerid-contents"></a>USB ContainerID 内容


USB **ContainerID**提供给全局唯一标识符 (UUID) 字符串的窗体中的操作系统。 **ContainerID**中包含 UUID **ContainerID**描述符。 一个**ContainerID**描述符是设备级 Microsoft 操作系统功能描述符。 在这种情况下，当操作系统请求 USB **ContainerID**，描述符请求 wValue 字段必须始终设置为零。 有关 Microsoft 操作系统功能描述符和描述符请求的详细信息，请参阅[Microsoft 操作系统 1.0 描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617519)。

一个**ContainerID**描述符包含的表头部分。

| 偏移量 | 字段          | 大小 | 在任务栏的搜索框中键入           | 描述                                                                                                                                                                                                                                                                                                                                                                                         |
|--------|----------------|------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0      | **dwLength**   | 4    | 无符号的 DWord | 长度，以字节为单位的整个**ContainerID**描述符。 此字段必须始终设置为从 0x18 的值。                                                                                                                                                                                                                                                                                   |
| 4      | **bcdVersion** | 2    | BCD            | 版本号**ContainerID**中二进制编码的十进制 (BCD)，其中每个半字节对应于一个数字的描述符。 最高有效字节 (MSB) 包含小数点，前面的两位数字，最低有效字节 (LSB) 包含小数点后两位数字。 例如，版本 1.00 表示为 0x0100。 此字段必须始终设置为 0x0100 中。 |
| 6      | **wIndex**     | 2    | Word           | 此字段始终设置为 6 的 USB **ContainerID**描述符。                                                                                                                                                                                                                                                                                                                                  |

 

一个**ContainerID**描述符包含 ContainerID 部分。

| 偏移量 | 字段            | 大小 | 在任务栏的搜索框中键入           | 描述           |
|--------|------------------|------|----------------|-----------------------|
| 0      | **bContainerID** | 16   | 无符号的 DWord | **ContainerID**数据。 |

 

设备制造商有责任确保设备的每个实例具有全局唯一的 16 字节值**ContainerID**。 此外，设备必须报告相同**ContainerID**提供支持每次值。
有几个已建立的算法用于生成 Uuid 与几乎为零的重复的可能性。 设备制造商可以选择最适合其需求的 UUID 生成算法。 并不重要，只要是唯一的结果使用的 UUID 生成算法。

## <a name="usb-containerid-syntax"></a>USB ContainerID 语法


一个**ContainerID**中 {xxxxxxxx xxxx-xxxx-xxxx-在左右加上} 标准的 UUID 字符串格式报告。 以下是有关 0 的 C B4 A7 固件中的示例表示 2c D1 7B 25 4F B5 73 A1 3A 97 5D DC 07 USB **ContainerID**，其格式为 {2CA7B40C-7BD1-4F25-B573-A13A975DDC07} UUID 字符串。

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

格式化为 UUID 字符串时，请注意第一个 8 字节的字节顺序的更改。

## <a name="microsoft-os-descriptor-changes"></a>Microsoft 操作系统描述符更改


若要保留旧**ContainerID**的功能，已添加到可用于指示对支持的 Microsoft 操作系统字符串描述符字段新标志**ContainerID**描述符。

Microsoft 操作系统字符串描述符的当前定义包含一个 1 字节填充的字段， **bPad**，通常设置为零的描述符的末尾。 为支持新的 USB 设备**ContainerID**，则**bPad**字段重新定义为标记字段**bFlags**。 此字段的 1 位用于指示支持**ContainerID**描述符。 表 3 介绍了 USB 设备的 Microsoft 操作系统字符串描述符字段。

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
<th>长度 （字节）</th>
<th>ReplTest1</th>
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
<td>描述符类型。 0x03 的值表示 Microsoft 操作系统字符串描述符。</td>
</tr>
<tr class="odd">
<td><strong>qwSignature</strong></td>
<td>14</td>
<td>‘MSFT100’</td>
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
<td><p>位 0:保留</p>
<p>1 位：<strong>ContainerID</strong>支持</p>
<ul>
<li>0:不支持<strong>ContainerID</strong></li>
<li>1：支持<strong>ContainerID</strong></li>
</ul>
<p>位 2 – 7:保留</p></td>
</tr>
</tbody>
</table>

 

当前传送支持 Microsoft 操作系统描述符，但不是支持的 USB 设备**ContainerID**描述符具有**bPad**字段设置为 0x00。 USB 集线器驱动程序不会查询此类设备的 USB **ContainerID**描述符。
## <a name="container-view-of-a-usb-multifunction-device"></a>USB 多功能设备的容器视图


**ContainerID**提供一些信息以合并多功能 USB 设备的设备。 图 1 显示了如何的示例中的多功能打印机的所有设备都合并到单个设备容器在产品内的所有单个设备使用相同**ContainerID**。

![多功能打印机中的所有设备的合并](images/containerid-multifunction.png)

通过合并有关多功能的 USB 设备的所有设备，物理产品可以显示为单个设备中设备和 Windows 7 中的打印机。 图 2 显示了 USB 多功能键盘和鼠标设备显示为单个设备中设备和打印机的示例。

![在设备和打印机的多功能设备](images/containerid-multifunction1.png)

## <a name="usb-containerid-hck-requirements"></a>USB ContainerID HCK 要求


设备制造商必须确保它们生成的设备的每个实例具有全局唯一**ContainerID**值，以便 Windows 可以成功合并的每个 USB 多功能设备的功能。 Windows 硬件认证 Windows 硬件认证工具包包含一项要求，说明 0034，用于 USB **ContainerID**如果在设备中实现。 如果设备实现 USB **ContainerID**、 Windows 硬件认证测试**ContainerID**作为 Microsoft 操作系统描述符的一部分测试，并检查是否**ContainerID**是全局唯一的值。 这些 Windows 硬件认证要求的更多详细信息，请参阅 Windows 硬件认证网站。

建议用于实现 USB **ContainerID**以下是有关设计、 制造，和交付 USB 设备的设备供应商的建议：

-   了解 Windows 7 如何改进支持多功能和使用的多个传输的 USB 设备**ContainerID**。 我们建议你先阅读"多功能设备支持和 Windows 7 中的设备容器分组。"
-   请确保每个 USB 设备上的序列号是唯一的。 Windows 硬件认证要求规定，是否你的设备包括序列号，序列号必须是唯一的设备的每个实例。
-   未提供**ContainerID**系统中内嵌的 USB 设备。 集成的 USB 设备应依赖于 ACPI BIOS 设置或 USB 集线器描述符**DeviceRemovable**位的端口。
-   请确保附加到系统的所有 USB 设备都具有唯一**ContainerID**值。 不共享**ContainerID**值或不同产品系列间的 USB 序列号。
-   请确保设置正确让你的设备的可移动设备功能。
    **请注意**  添加 USB 的设备供应商**ContainerID**描述符添加到以前传送的 USB 设备必须递增设备发行版号 (**bcdDevice**) 中的设备设备描述符。 这是必需的因为 USB 集线器驱动程序缓存 Microsoft OS 描述符 （或缺乏一个），它基于设备的供应商 ID、 产品 ID 和设备发行版号的字符串。 如果您也不会增加设备发行版号，中心驱动程序不会查询 USB **ContainerID**的新设备，如果它之前枚举实例具有相同的供应商 ID、 产品 ID 和设备发行版号的设备不支持 USB **ContainerID**描述符。

     

## <a name="related-topics"></a>相关主题
[针对 Windows 构建的 USB 设备](building-usb-devices-for-windows.md)  
[USB 设备的容器 Id](https://msdn.microsoft.com/library/windows/hardware/ff540084)  



