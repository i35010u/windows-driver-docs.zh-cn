---
title: 底片扫描仪的可选 WIA 项属性
description: 底片扫描仪的可选 WIA 项属性
ms.assetid: 6c17deed-7840-4ec0-bc19-d695b3e80c38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13997f23e3b9301ec3b7a88160a56991f59c4ca5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376545"
---
# <a name="optional-wia-item-properties-for-film-scanners"></a>底片扫描仪的可选 WIA 项属性





以下 WIA 属性都可以选择支持 WIA 电影扫描程序项：

[**WIA\_IPA\_FILENAME\_EXTENSION**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-filename-extension)

[**WIA\_IPA\_RAW\_BITS\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)

[**WIA\_IPS\_AUTO\_DESKEW**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-auto-deskew)

[**WIA\_IPS\_DESKEW\_X**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-x)

[**WIA\_IPS\_反扭曲\_Y**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-y)

[**WIA\_IPS\_LAMP**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-lamp)

[**WIA\_IPS\_LAMP\_AUTO\_OFF**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-lamp-auto-off)

[**WIA\_IPS\_预览\_类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview-type)

[**WIA\_IP\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation)

[**WIA\_IP\_分段**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-segmentation)

[**WIA\_IPS\_显示\_预览\_控件**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-show-preview-control)

[**WIA\_IPS\_支持\_子\_项\_创建**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-supports-child-item-creation)

[**WIA\_IP\_阈值**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)

[**WIA\_IPS\_WARM\_UP\_TIME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-warm-up-time)

[**WIA\_IPS\_XSCALING**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xscaling)

[**WIA\_IPS\_YSCALING**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yscaling)

**请注意**   [ **WIA\_IPA\_RAW\_位\_每\_通道**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)属性是必需的如果WiaImgFmt\_支持原始格式。 [ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性必须支持 WiaImgFmt\_BMP 格式。 [ **WIA\_IPS\_阈值**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)时，属性是必需[ **WIA\_IPA\_深度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)属性设置为 1 BPP 时，或者当[ **WIA\_IPA\_数据类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性设置为 WIA\_数据\_阈值。

 

 

 




