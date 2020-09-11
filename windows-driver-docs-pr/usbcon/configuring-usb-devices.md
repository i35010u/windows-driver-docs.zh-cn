---
description: 本节中的主题介绍客户端驱动程序必须如何配置其设备。
title: 在 USB 驱动程序中选择 USB 配置概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e58485efce4759fd2f566aa9434d3cc59387ce
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010619"
---
# <a name="overview-of-selecting-a-usb-configuration-in-usb-drivers"></a>选择 USB 驱动程序中的 USB 配置的概述


本节中的主题介绍客户端驱动程序必须如何配置其设备。

USB 设备以一系列称为 *USB 配置*的接口的形式公开其功能。 每个接口都由一个或多个备用设置组成，每个备用设置由一组终结点组成。 设备至少必须提供一个配置，但它可以提供多个配置，这些配置是设备可执行的操作的独立定义。 有关配置描述符的详细信息，请参阅 [USB 配置描述符](usb-configuration-descriptors.md)。

设备配置指的是客户端驱动程序执行的任务，用于选择 USB 配置和每个接口中的备用接口。 将 i/o 请求发送到设备之前，客户端驱动程序必须读取设备的配置，分析信息，并选择适当的配置。 为了使设备正常工作，客户端驱动程序必须至少选择一个支持的配置。

基于 WDM 的客户端驱动程序可以选择 USB 设备中的任何配置。

如果客户端驱动程序基于 [内核模式驱动程序框架](../wdf/index.md) 或 [用户模式驱动程序框架](../wdf/index.md)，则应使用各自的框架接口来配置 USB 设备。 如果使用 Microsoft Visual Studio Professional 2012 附带的 USB 模板，则模板代码将选择每个接口中的第一个配置和默认备用设置。

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
<td><p><a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何选择 USB 设备的配置</a></p></td>
<td><p>在本主题中，你将了解如何在通用串行总线 (USB) 设备中选择配置。</p></td>
</tr>
<tr class="even">
<td><p><a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 界面中选择备用设置</a></p></td>
<td><p>本主题介绍发出选择接口请求以激活 USB 接口中的替代设置的步骤。 在选择 USB 配置之后，客户端驱动程序必须发出此请求。 默认情况下，选择配置还会激活该配置的每个接口中的第一个备用设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md" data-raw-source="[Configuring Usbccgp.sys to Select a Non-Default USB Configuration](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)">配置 Usbccgp.sys，选择非默认 USB 配置</a></p></td>
<td><p>本主题提供有关配置 Usbccgp.sys 选择 USB 配置方式的注册表设置的信息。 本主题还介绍 Usbccgp.sys 如何处理客户端驱动程序发送的控制复合设备功能之一的选择配置请求。</p></td>
</tr>
</tbody>
</table>

 

有关与需要下载固件的设备配置相关的特殊注意事项的信息，请参阅 [配置需要固件下载的 USB 设备](configuring-usb-devices-that-require-firmware-downloads.md)。

## <a name="limitations-for-selecting-a-configuration"></a>选择配置的限制


如果客户端驱动程序使用 WDF 对象，或者设备是否有单个接口或多个接口，则会应用某些限制。 更改默认配置之前，请考虑以下限制：

-   复合设备的客户端驱动程序（通过 [USB 通用父驱动程序](usb-common-class-generic-parent-driver.md) ( # A0) 管理接口或接口集合无法更改设备的配置值。 但是，客户端驱动程序可以将 Usbccgp.sys 配置为选择除第一个 (默认) 配置以外的其他配置。 有关详细信息，请参阅 [配置 Usbccgp.sys 以选择非默认的 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)。
-   使用框架的 [USB I/o 目标](../wdf/usb-i-o-targets.md) 的基于 KMDF 的客户端驱动程序只能选择第一个配置。
-   [WinUSB](winusb.md) 仅支持第一个配置。
-   类驱动程序通常不支持多个配置。 如果设备实现了由 USB 类规范定义的类，请参阅 [Usb 技术](https://go.microsoft.com/fwlink/p/?linkid=8769) 网站获取有关设备类和类规范的信息。 Microsoft 为支持的 USB 设备类提供类驱动程序。 有关详细信息，请参阅[支持的 USB 设备类的驱动程序](supported-usb-classes.md)。

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)  
[USB 配置描述符](usb-configuration-descriptors.md)  
[使用 USB 设备](../wdf/working-with-usb-devices.md)  
[在 UMDF 中使用 USB 接口](../wdf/working-with-usb-interfaces-in-umdf-1-x-drivers.md)