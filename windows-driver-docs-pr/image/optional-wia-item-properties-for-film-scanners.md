---
title: 底片扫描仪的可选 WIA 项属性
description: 底片扫描仪的可选 WIA 项属性
ms.assetid: 6c17deed-7840-4ec0-bc19-d695b3e80c38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d5a87679d936be9e5916991e8df110b57553efe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357883"
---
# <a name="optional-wia-item-properties-for-film-scanners"></a>底片扫描仪的可选 WIA 项属性





以下 WIA 属性都可以选择支持 WIA 电影扫描程序项：

[**WIA\_IPA\_FILENAME\_EXTENSION**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

[**WIA\_IPA\_RAW\_BITS\_每\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff551641)

[**WIA\_IPS\_AUTO\_DESKEW**](https://msdn.microsoft.com/library/windows/hardware/ff552564)

[**WIA\_IPS\_DESKEW\_X**](https://msdn.microsoft.com/library/windows/hardware/ff552581)

[**WIA\_IPS\_反扭曲\_Y**](https://msdn.microsoft.com/library/windows/hardware/ff552587)

[**WIA\_IPS\_LAMP**](https://msdn.microsoft.com/library/windows/hardware/ff552603)

[**WIA\_IPS\_LAMP\_AUTO\_OFF**](https://msdn.microsoft.com/library/windows/hardware/ff552605)

[**WIA\_IPS\_预览\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff552646)

[**WIA\_IP\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff552648)

[**WIA\_IP\_分段**](https://msdn.microsoft.com/library/windows/hardware/ff552649)

[**WIA\_IPS\_显示\_预览\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff552652)

[**WIA\_IPS\_支持\_子\_项\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff552653)

[**WIA\_IP\_阈值**](https://msdn.microsoft.com/library/windows/hardware/ff552655)

[**WIA\_IPS\_WARM\_UP\_TIME**](https://msdn.microsoft.com/library/windows/hardware/ff552660)

[**WIA\_IPS\_XSCALING**](https://msdn.microsoft.com/library/windows/hardware/ff552667)

[**WIA\_IPS\_YSCALING**](https://msdn.microsoft.com/library/windows/hardware/ff552676)

**请注意**   [ **WIA\_IPA\_RAW\_位\_每\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff551641)属性是必需的如果WiaImgFmt\_支持原始格式。 [ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)属性必须支持 WiaImgFmt\_BMP 格式。 [ **WIA\_IPS\_阈值**](https://msdn.microsoft.com/library/windows/hardware/ff552655)时，属性是必需[ **WIA\_IPA\_深度**](https://msdn.microsoft.com/library/windows/hardware/ff551546)属性设置为 1 BPP 时，或者当[ **WIA\_IPA\_数据类型**](https://msdn.microsoft.com/library/windows/hardware/ff551543)属性设置为 WIA\_数据\_阈值。

 

 

 




