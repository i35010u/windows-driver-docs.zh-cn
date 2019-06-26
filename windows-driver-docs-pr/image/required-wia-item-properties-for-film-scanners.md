---
title: 底片扫描仪的必需 WIA 项属性
description: 底片扫描仪的必需 WIA 项属性
ms.assetid: f87e1bfc-6d85-4aba-a2ad-e491f997a3ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ff6e572d4fa342d55249e4ca73cc6cbf7da9f7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374265"
---
# <a name="required-wia-item-properties-for-film-scanners"></a>底片扫描仪的必需 WIA 项属性





支持以下 WIA 属性需要 WIA 电影扫描程序项：

[**WIA\_IPA\_访问\_权限**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-access-rights)

[**WIA\_IPA\_BITS\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bits-per-channel)

[**WIA\_IPA\_压缩**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-compression)

[**WIA\_IPA\_CHANNELS\_PER\_PIXEL**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-channels-per-pixel)

[**WIA\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)

[**WIA\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)

[**WIA\_IPS\_FILM\_SCAN\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-film-scan-mode)

[**WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)

[**WIA\_IPA\_FULL\_ITEM\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-full-item-name)

[**WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)

[**WIA\_IPA\_ITEM\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-name)

[**WIA\_IPA\_ITEM\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)

[**WIA\_IPA\_PREFERRED\_FORMAT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-preferred-format)

[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)

[**WIA\_IP\_亮度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-brightness)

[**WIA\_IPS\_CONTRAST**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-contrast)

[**WIA\_IPS\_CUR\_INTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-cur-intent)

[**WIA\_IPS\_MAX\_HORIZONTAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-horizontal-size)

[**WIA\_IPS\_MAX\_VERTICAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-vertical-size)

[**WIA\_IPS\_MIN\_HORIZONTAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-horizontal-size)

[**WIA\_IPS\_MIN\_VERTICAL\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-vertical-size)

[**WIA\_IPS\_OPTICAL\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-xres)

[**WIA\_IPS\_OPTICAL\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-yres)

[**WIA\_IPS\_PHOTOMETRIC\_INTERP**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-photometric-interp)

[**WIA\_IP\_预览**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview)

[**WIA\_IPS\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)

[**WIA\_IPS\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)

[**WIA\_IPS\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)

[**WIA\_IPS\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)

[**WIA\_IPS\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)

[**WIA\_IPS\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)

**请注意**   [ **WIA\_IPA\_RAW\_位\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)属性是必需的如果WiaImgFmt\_支持原始格式。 [ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性必须支持 WiaImgFmt\_BMP 格式。 [ **WIA\_IPS\_阈值**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)时，属性是必需[ **WIA\_IPA\_深度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)属性设置为 1 的位每像素 (BPP) 时，或者当[ **WIA\_IPA\_数据类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性设置为 WIA\_数据\_阈值。

 

 

 




