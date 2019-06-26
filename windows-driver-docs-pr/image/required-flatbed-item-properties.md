---
title: 必需平板项属性
description: 必需平板项属性
ms.assetid: 5af295de-b5ad-47c7-b1db-9d5685ed8d19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbebc9a8ff381d9aab0efdeed14bbccd845994a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374281"
---
# <a name="required-flatbed-item-properties"></a>必需平板项属性





支持以下 WIA 属性需要 WIA 平板扫描仪项：

[**WIA\_IPA\_访问\_权限**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-access-rights)

[**WIA\_IPA\_BITS\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bits-per-channel)

[**WIA\_IPA\_缓冲区\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)

[**WIA\_IPA\_CHANNELS\_PER\_PIXEL**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-channels-per-pixel)

[**WIA\_IPA\_颜色\_配置文件**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-color-profile)

[**WIA\_IPA\_压缩**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-compression)

[**WIA\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)

[**WIA\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)

[**WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)

[**WIA\_IPA\_FULL\_ITEM\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-full-item-name)

[**WIA\_IPA\_ICM\_PROFILE\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-icm-profile-name)

[**WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)

[**WIA\_IPA\_ITEM\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-name)

[**WIA\_IPA\_ITEM\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)

[**WIA\_IPS\_MAX\_HORIZONTAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-horizontal-size)

[**WIA\_IPS\_MAX\_VERTICAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-vertical-size)

[**WIA\_IPS\_MIN\_HORIZONTAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-horizontal-size)

[**WIA\_IPS\_MIN\_VERTICAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-vertical-size)

[**WIA\_IPA\_数\_OF\_行**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-number-of-lines)

[**WIA\_IPA\_PIXELS\_PER\_LINE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-pixels-per-line)

[**WIA\_IPA\_PLANAR**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-planar)

[**WIA\_IPA\_PREFERRED\_FORMAT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-preferred-format)

[**WIA\_IPA\_PROP\_STREAM\_COMPAT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-prop-stream-compat-id)

[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)

[**WIA\_IP\_亮度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-brightness)

[**WIA\_IPS\_CONTRAST**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-contrast)

[**WIA\_IPS\_CUR\_INTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-cur-intent)

[**WIA\_IPS\_OPTICAL\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-xres)

[**WIA\_IPS\_OPTICAL\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-yres)

[**WIA\_IP\_预览**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview)

[**WIA\_IPS\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)

[**WIA\_IPS\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)

[**WIA\_IPS\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)

[**WIA\_IPS\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)

[**WIA\_IPS\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)

[**WIA\_IPS\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)

**请注意**   [ **WIA\_IPA\_RAW\_位\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)属性是必需的如果WiaImgFmt\_支持原始格式。 [ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性必须支持 WiaImgFmt\_BMP 格式。 [ **WIA\_IPS\_阈值**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)时，属性是必需[ **WIA\_IPA\_深度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)属性设置为 1 位 / 像素 (BPP) 时，或者当[ **WIA\_IPA\_数据类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性设置为 WIA\_数据\_阈值。

 

 

 




