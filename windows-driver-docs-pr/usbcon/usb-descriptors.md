---
Description: USB 设备提供了有关其自身的数据结构称为 USB 描述符中的信息。 本部分提供有关客户端驱动程序可以从 USB 设备中获取的各种描述符信息。
title: USB 描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa76f5ebd1a17daea749c8fe0eb781df4b9f2407
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360158"
---
# <a name="usb-descriptors"></a>USB 描述符


USB 设备提供了有关其自身在名为的数据结构中的信息*USB 描述符*。 本部分提供有关客户端驱动程序可以从 USB 设备中获取的各种描述符信息。




主机通过发送各种标准控件请求从已连接的设备获取描述符 (获取\_描述符请求) 到默认终结点。 这些请求指定的类型描述符来检索。 此类请求的响应，设备发送描述符包括有关设备、 其配置、 接口和相关的终结点的信息。 *设备描述符*包含整个设备的相关信息。 *配置描述符*包含有关每个设备配置信息。 *字符串描述符*包含 Unicode 文本字符串。

每个 USB 设备公开的设备描述符，指示设备的类信息、 供应商和产品标识符，以及多个配置。 每个配置还公开其配置描述符，该值指示大量接口和功耗特征。 每个接口公开其包含类和数量的终结点信息的替代设置的每个接口描述符。 每个接口中的每个终结点公开终结点，描述符可指明终结点类型和最大数据包大小。

例如，请考虑 OSR FX2 板设备布局中所述[USB 设备布局](usb-device-layout.md)。 在设备级别，设备会公开设备描述符和默认终结点的终结点描述符。 在配置级别，设备配置 0 公开配置描述符。 在接口级别，它公开一个接口描述符为备用设置 0。 为终结点级别，它公开三个终结点描述符。

## <a name="in-this-section"></a>本节内容


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
<td><p>设备描述符包含有关 USB 设备作为一个整体的信息。 本主题介绍<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_device_descriptor" data-raw-source="[&lt;strong&gt;USB_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_device_descriptor)"> <strong>USB_DEVICE_DESCRIPTOR</strong> </a>结构，并包含有关客户端驱动程序如何发送 get 描述符请求以获取设备描述符信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[USB configuration descriptors](usb-configuration-descriptors.md)">USB 配置描述符</a></p></td>
<td><p>USB 设备公开的接口称为 USB 配置一系列的窗体中的其功能。 每个接口由一个或多个备用的设置，和每个备用设置由一组终结点组成。 本主题介绍与 USB 配置相关联的各种描述符。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-string-descriptors.md" data-raw-source="[USB String Descriptors](usb-string-descriptors.md)">USB 字符串描述符</a></p></td>
<td><p>设备、 配置和接口描述符可能包含对字符串描述符的引用。 本主题介绍如何从设备获取特定字符串描述符。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-interface-association-descriptor.md" data-raw-source="[USB Interface Association Descriptor](usb-interface-association-descriptor.md)">USB 接口关联描述符</a></p></td>
<td><p>USB 接口关联描述符 (IAD) 允许设备连接到属于函数的组接口。 本主题介绍客户端驱动程序可以确定设备是否包含一个函数 IAD。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 设备布局](usb-device-layout.md)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



