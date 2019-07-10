---
Description: 在本部分中的主题介绍客户端驱动程序必须配置其设备的方式。
title: USB 驱动程序概述中选择 USB 配置概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 395cbcf02cecc65194073f52b6cb8248c6d26133
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716959"
---
# <a name="overview-of-selecting-a-usb-configuration-in-usb-drivers"></a>在 USB 驱动程序选择 USB 配置的概述


在本部分中的主题介绍客户端驱动程序必须配置其设备的方式。

USB 设备公开其功能中的接口名为一系列的窗体*USB 配置*。 每个接口由一个或多个备用的设置，和每个备用设置由一组终结点组成。 设备必须提供至少一个配置，但它可以提供是互相排斥定义的设备可以执行的多个配置。 有关配置描述符的详细信息，请参阅[USB 配置描述符](usb-configuration-descriptors.md)。

设备配置是指客户端驱动程序执行要选择的每个接口中的 USB 配置和备用接口的任务。 前向设备发送的 I/O 请求，客户端驱动程序必须读取设备的配置、 分析信息，并选择相应的配置。 客户端驱动程序必须选择至少一个支持的配置以使设备正常工作。

WDM 基于客户端驱动程序可以选择任何配置 USB 设备中。

如果您的客户端驱动程序基于[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)或[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)，应使用各自的框架的接口来配置 USB 设备。 如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码将在每个接口中选择的第一个配置和默认备用设置。

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
<td><p><a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何选择 USB 设备的配置</a></p></td>
<td><p>在本主题中，您将学习有关如何选择一种配置中的通用串行总线 (USB) 设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 界面中选择一项备用设置</a></p></td>
<td><p>本主题介绍发出选择接口请求以激活一项备用设置 USB 接口中的步骤。 客户端驱动程序必须选择 USB 配置后发出此请求。 默认情况下，选择一个配置，还会激活该配置中每个接口中的第一个备用设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md" data-raw-source="[Configuring Usbccgp.sys to Select a Non-Default USB Configuration](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)">配置 Usbccgp.sys 选择非默认 USB 配置</a></p></td>
<td><p>本主题提供 Usbccgp.sys 选择 USB 配置注册表设置配置的方式的信息。 本主题还介绍如何 Usbccgp.sys 处理发送的控制功能的复合设备之一的客户端驱动程序选择配置请求。</p></td>
</tr>
</tbody>
</table>

 

需要固件下载设备配置相关的特殊注意事项的信息，请参阅[配置 USB 设备，需要固件下载](configuring-usb-devices-that-require-firmware-downloads.md)。

## <a name="limitations-for-selecting-a-configuration"></a>选择配置的限制


如果客户端驱动程序使用 WDF 对象或设备有一个单一的界面或多个接口存在一些限制。 更改默认配置之前，请考虑以下限制：

-   用于管理接口或通过接口集合的复合设备的客户端驱动程序[USB 通用父驱动程序](usb-common-class-generic-parent-driver.md)(Usbccgp.sys) 不能更改设备的配置值。 但是，客户端驱动程序可以配置 Usbccgp.sys 选择以外的第一个 （默认值） 配置的配置。 有关详细信息，请参阅[配置 Usbccgp.sys 选择非默认 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)。
-   使用框架的 KMDF 基于客户端驱动程序[USB I/O 目标](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets)可以选择仅第一个配置。
-   [WinUSB](winusb.md)仅支持第一个配置。
-   类驱动程序经常缺少对多个配置的支持。 如果你的设备实现由 USB 类规范定义的类，请参阅[USB 技术](https://go.microsoft.com/fwlink/p/?linkid=8769)网站以获取有关设备类和类规范的信息。 Microsoft 提供了受支持的 USB 设备类的类驱动程序。 有关详细信息，请参阅[支持的 USB 设备类的驱动程序](supported-usb-classes.md)。

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)  
[USB 配置描述符](usb-configuration-descriptors.md)  
[使用 USB 设备](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices)  
[使用 USB 接口在 UMDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers)  



