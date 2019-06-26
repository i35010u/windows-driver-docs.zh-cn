---
title: 进行原始格式传输所需的属性验证
description: 进行原始格式传输所需的属性验证
ms.assetid: ad58f94e-d59e-4d04-be27-cc87f89f3d76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ee353bc505b536adbb95e04ea999b0f060d782e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376507"
---
# <a name="property-validation-for-raw-format-transfers"></a>进行原始格式传输所需的属性验证


驱动程序必须验证之前的原始格式的数据传输的 WIA 属性设置。 必须按如下所示设置 WIA 属性：

<a href="" id="wia-ips-xpos--wia-ips-ypos"></a>[**WIA\_IPS\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)， [ **WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)  
这些属性设置相同的 RAW 相同，均为其他图像格式。 这些属性包含以像素为单位的所选图像的左上角的坐标

<a href="" id="wia-ips-xres--wia-ips-yres"></a>[**WIA\_IPS\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)， [ **WIA\_IP\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)  
这些属性设置相同的 RAW 相同，均为其他图像格式。 这些属性 （分别） 包含当前水平和垂直分辨率，以像素为单位的每英寸点数，设备

<a href="" id="wia-ips-xextent--wia-ips-yextent"></a>[**WIA\_IPS\_大 XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)， [ **WIA\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)  
应用程序设置这些属性读取和更新驱动程序。 由于属性可能会更改从其原始值，该应用程序必须读取处理原始流时，这些属性中存储的值。

<a href="" id="wia-ipa-depth"></a>[**WIA\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)  
此属性包含的每个像素的位数。 驱动程序应用程序集时设置此属性的值[ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)到**WiaImgFmt\_RAW**。 所有 WIA 中的项的总和\_IPA\_RAW\_BITS\_每\_通道属性必须等于 WIA 中存储的号\_IPA\_DEPTH 属性。 WIA\_IPA\_深度是可写，如果该驱动程序支持多个配置。 例如，对于支持 32 位 / 像素和 48 位 / 像素配置驱动程序，该应用程序可以选择一种设置，并且该驱动程序应设置 WIA\_IPA\_RAW\_BITS\_每\_通道和关联的属性相应地。

<a href="" id="wia-ipa-raw-bits-per-channel"></a>[**WIA\_IPA\_RAW\_BITS\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)  
此属性设置为值的响应中的驱动程序通过**WiaImgFmt\_RAW**中 WIA\_IPA\_FORMAT 属性，并当更新 WIA\_IPA\_数据类型是更改。 所有条目 WIA\_IPA\_RAW\_BITS\_每\_通道必须等于每像素存储在 WIA 的比特数\_IPA\_深度。

<a href="" id="wia-ipa-channels-per-pixel"></a>[**WIA\_IPA\_CHANNELS\_PER\_PIXEL**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-channels-per-pixel)  
此属性由驱动程序添加到每个像素的所选原始通道数设置子类型中 WIA\_IPA\_数据类型。

<a href="" id="wia-ipa-datatype"></a>[**WIA\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)  
当 WIA\_IPA\_格式设置为**WiaImgFmt\_RAW**，驱动程序将此属性设置为默认值。 该驱动程序还确定该应用程序可以选择要更改默认值的允许值的列表。 WIA\_IPA\_驱动程序选择的数据类型默认值; 它可以是任何设备允许的值。

<a href="" id="wia-ipa-bytes-per-line"></a>[**WIA\_IPA\_BYTES\_PER\_LINE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bytes-per-line)  
必须由根据 WIA 微型驱动程序更新\_IPA\_格式和 WIA\_IPA\_数据类型设置。

<a href="" id="wia-ipa-item-size"></a>[**WIA\_IPA\_ITEM\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)  
必须为零。

 

 




