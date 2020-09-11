---
description: USB 设备在称为 USB 描述符的数据结构中提供自身的相关信息。 本部分提供有关客户端驱动程序可以从 USB 设备获取的各种描述符的信息。
title: USB 描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59d02f1f9fe6fe1f8f6c00f8232193f01075ae26
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010097"
---
# <a name="usb-descriptors"></a>USB 描述符


USB 设备在称为 *USB 描述符*的数据结构中提供自身的相关信息。 本部分提供有关客户端驱动程序可以从 USB 设备获取的各种描述符的信息。




主机通过发送各种标准控制请求 (获取 \_) 到默认终结点的描述符请求，从附加的设备中获取描述符。 这些请求指定要检索的描述符类型。 为响应此类请求，设备会发送包含有关设备、其配置、接口和相关终结点的信息的描述符。 *设备描述符* 包含有关整个设备的信息。 *配置描述符* 包含有关每个设备配置的信息。 *字符串描述符* 包含 Unicode 文本字符串。

每个 USB 设备都公开一个设备描述符，用于指示设备的类信息、供应商和产品标识符，以及配置数。 每个配置都公开其配置描述符，指示接口和电源特征的数目。 每个接口都公开其每个替代设置的接口描述符，其中包含有关类的信息和终结点的数目。 每个接口中的每个终结点都公开终结点描述符，指示终结点类型和最大数据包大小。

例如，请考虑 [USB 设备布局](usb-device-layout.md)中所述的 OSR FX2 板设备布局。 在设备级别，设备将公开默认终结点的设备描述符和终结点描述符。 在配置级别，设备会为配置0公开配置描述符。 在接口级别，它为备用设置0公开了一个接口描述符。 在终结点级别，它公开了三个终结点说明符。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="usb-device-descriptors.md" data-raw-source="[USB device descriptors](usb-device-descriptors.md)">USB 设备描述符</a></p></td>
<td><p>设备描述符同时包含有关 USB 设备的信息。 本主题介绍 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor" data-raw-source="[&lt;strong&gt;USB_DEVICE_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)"><strong>USB_DEVICE_DESCRIPTOR</strong></a> 的结构，并包括有关客户端驱动程序如何发送获取描述符请求以获取设备描述符的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[USB configuration descriptors](usb-configuration-descriptors.md)">USB 配置描述符</a></p></td>
<td><p>USB 设备以一系列称为 USB 配置的接口的形式公开其功能。 每个接口都由一个或多个备用设置组成，每个备用设置由一组终结点组成。 本主题介绍与 USB 配置相关的各种描述符。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-string-descriptors.md" data-raw-source="[USB String Descriptors](usb-string-descriptors.md)">USB 字符串描述符</a></p></td>
<td><p>设备、配置和接口描述符可能包含对字符串描述符的引用。 本主题介绍如何从设备获取特定字符串描述符。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-interface-association-descriptor.md" data-raw-source="[USB Interface Association Descriptor](usb-interface-association-descriptor.md)">USB 接口关联描述符</a></p></td>
<td><p>USB 接口关联描述符 (IAD) 允许设备对属于某个函数的接口进行分组。 本主题介绍客户端驱动程序如何确定设备是否包含用于函数的 IAD。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 设备布局](usb-device-layout.md)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)