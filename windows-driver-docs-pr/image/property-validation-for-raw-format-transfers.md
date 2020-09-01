---
title: 进行原始格式传输所需的属性验证
description: 进行原始格式传输所需的属性验证
ms.assetid: ad58f94e-d59e-4d04-be27-cc87f89f3d76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff24e68928e9650c95f0850579125c8eb4cd94ef
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186467"
---
# <a name="property-validation-for-raw-format-transfers"></a>进行原始格式传输所需的属性验证


驱动程序必须在原始格式数据传输之前验证 WIA 属性设置。 必须按如下所示设置 WIA 属性：

<a href="" id="wia-ips-xpos--wia-ips-ypos"></a>[**WIA \_IP \_ XPOS**](./wia-ips-xpos.md)， [ **WIA \_ IP \_ YPOS**](./wia-ips-ypos.md)  
对于原始属性，这些属性的设置与其他图像格式相同。 这些属性包含所选图像的左上角的坐标（以像素为单位）

<a href="" id="wia-ips-xres--wia-ips-yres"></a>[**WIA \_IP \_ XRES**](./wia-ips-xres.md)， [ **WIA \_ IP \_ YRES**](./wia-ips-yres.md)  
对于原始属性，这些属性的设置与其他图像格式相同。 这些属性分别包含设备的当前水平和垂直 () 的分辨率（以每英寸像素为单位）

<a href="" id="wia-ips-xextent--wia-ips-yextent"></a>[**WIA \_IP \_ XEXTENT**](./wia-ips-xextent.md)， [ **WIA \_ IP \_ YEXTENT**](./wia-ips-yextent.md)  
这些属性由应用程序设置，并由驱动程序进行读取和更新。 因为属性可能会更改为其原始值，所以，应用程序在处理原始流时必须读取存储在这些属性中的值。

<a href="" id="wia-ipa-depth"></a>[**WIA \_ IPA \_ 深度**](./wia-ipa-depth.md)  
此属性包含每个像素的位数。 当应用程序将 [**WIA \_ IPA \_ 格式**](./wia-ipa-format.md) 设置为 **WiaImgFmt \_ RAW**时，驱动程序将设置此属性的值。 WIA IPA 的每个通道的原始位属性中的所有项的总和 \_ \_ \_ \_ \_ 必须等于 wia \_ IPA DEPTH 属性中存储的数字 \_ 。 \_ \_ 如果驱动程序支持多个配置，WIA IPA 深度是可写的。 例如，对于每个像素支持32位的驱动程序和每像素配置48位，应用程序可以选择一项设置，驱动程序应为 \_ \_ 每个通道设置 WIA IPA 原始 \_ 位 \_ \_ 并相应地设置关联的属性。

<a href="" id="wia-ipa-raw-bits-per-channel"></a>[**WIA \_ IPA \_ \_ \_ 每通道原始 \_ 位数**](./wia-ipa-raw-bits-per-channel.md)  
此属性由驱动程序设置，以响应 WIA IPA FORMAT 属性中的 **WiaImgFmt \_ RAW** 值 \_ \_ ，并在 wia \_ IPA \_ 数据类型发生更改时进行更新。 WIA IPA 的每个通道的每个字节的所有条目 \_ \_ \_ \_ \_ 必须等于 wia IPA 深度中存储的每个像素的位数 \_ \_ 。

<a href="" id="wia-ipa-channels-per-pixel"></a>[**WIA \_ IPA \_ \_ 每像素通道数 \_**](./wia-ipa-channels-per-pixel.md)  
此属性由驱动程序设置为 WIA \_ IPA 数据类型中所选原始子类型的每个像素的通道数 \_ 。

<a href="" id="wia-ipa-datatype"></a>[**WIA \_ IPA \_ 数据类型**](./wia-ipa-datatype.md)  
当 WIA \_ IPA \_ 格式设置为 **WiaImgFmt \_ RAW**时，驱动程序将此属性设置为默认值。 该驱动程序还决定了允许的值的列表，应用程序可以选择这些值来更改默认值。 WIA \_ IPA \_ DATATYPE 默认值是由驱动程序选择的，它可以是设备允许的任何值。

<a href="" id="wia-ipa-bytes-per-line"></a>[**WIA \_ IPA \_ 字节 \_ / \_ 行**](./wia-ipa-bytes-per-line.md)  
必须由微型驱动程序根据 WIA \_ IPA \_ 格式和 wia \_ IPA \_ 数据类型设置进行更新。

<a href="" id="wia-ipa-item-size"></a>[**WIA \_ IPA \_ 项 \_ 大小**](./wia-ipa-item-size.md)  
必须为零。

 

