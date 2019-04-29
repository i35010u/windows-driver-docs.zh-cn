---
title: 送纸器扫描仪的必需 WIA 项属性
description: 送纸器扫描仪的必需 WIA 项属性
ms.assetid: f9868f05-3c1f-4042-9820-9c1c38af3432
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fc7461b14e5b7be301910ceafe97aa4776da724
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375843"
---
# <a name="required-wia-item-properties-for-feeder-scanners"></a>送纸器扫描仪的必需 WIA 项属性





支持以下 WIA 属性需要 WIA 送纸器扫描程序项：

[**WIA\_DPS\_文档\_处理\_选择**](https://msdn.microsoft.com/library/windows/hardware/ff551384)

[**WIA\_DPS\_PAGE\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff551417)

[**WIA\_IPA\_访问\_权限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

[**WIA\_IPA\_BITS\_每\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff551526)

[**WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)

[**WIA\_IPA\_CHANNELS\_PER\_PIXEL**](https://msdn.microsoft.com/library/windows/hardware/ff551535)

[**WIA\_IPA\_压缩**](https://msdn.microsoft.com/library/windows/hardware/ff551540)

[**WIA\_IPA\_DATATYPE**](https://msdn.microsoft.com/library/windows/hardware/ff551543)

[**WIA\_IPA\_DEPTH**](https://msdn.microsoft.com/library/windows/hardware/ff551546)

[**WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_FULL\_ITEM\_NAME**](https://msdn.microsoft.com/library/windows/hardware/ff551561)

[**WIA\_IPA\_ITEM\_NAME**](https://msdn.microsoft.com/library/windows/hardware/ff551590)

[**WIA\_IPA\_ITEM\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff551594)

[**WIA\_IPA\_PREFERRED\_FORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

[**WIA\_IP\_亮度**](https://msdn.microsoft.com/library/windows/hardware/ff552567)

[**WIA\_IPS\_CONTRAST**](https://msdn.microsoft.com/library/windows/hardware/ff552573)

[**WIA\_IPS\_CUR\_INTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552579)

[**WIA\_IPS\_MAX\_HORIZONTAL\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff552607)

[**WIA\_IPS\_MAX\_VERTICAL\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff552611)

[**WIA\_IPS\_MIN\_HORIZONTAL\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff552612)

[**WIA\_IPS\_MIN\_VERTICAL\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff552614)

[**WIA\_IPS\_OPTICAL\_XRES**](https://msdn.microsoft.com/library/windows/hardware/ff552620)

[**WIA\_IPS\_OPTICAL\_YRES**](https://msdn.microsoft.com/library/windows/hardware/ff552622)

[**WIA\_IPS\_PAGES**](https://msdn.microsoft.com/library/windows/hardware/ff552630)

[**WIA\_IPS\_PAGE\_HEIGHT**](https://msdn.microsoft.com/library/windows/hardware/ff552632)

[**WIA\_IPS\_PAGE\_WIDTH**](https://msdn.microsoft.com/library/windows/hardware/ff552636)

[**WIA\_IPS\_PHOTOMETRIC\_INTERP**](https://msdn.microsoft.com/library/windows/hardware/ff552640)

[**WIA\_IPS\_XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)

[**WIA\_IPS\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)

[**WIA\_IPS\_XRES**](https://msdn.microsoft.com/library/windows/hardware/ff552665)

[**WIA\_IPS\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)

[**WIA\_IPS\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)

[**WIA\_IPS\_YRES**](https://msdn.microsoft.com/library/windows/hardware/ff552673)

**请注意**   [ **WIA\_IPA\_RAW\_位\_每\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff551641)属性是必需的如果WiaImgFmt\_支持原始格式。 [ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)属性必须支持 WiaImgFmt\_BMP 格式。 [ **WIA\_IPS\_阈值**](https://msdn.microsoft.com/library/windows/hardware/ff552655)时，属性是必需[ **WIA\_IPA\_深度**](https://msdn.microsoft.com/library/windows/hardware/ff551546)属性设置为 1 的位每像素 (BPP) 时，或者当[ **WIA\_IPA\_数据类型**](https://msdn.microsoft.com/library/windows/hardware/ff551543)属性设置为 WIA\_数据\_阈值。

 

 

 




