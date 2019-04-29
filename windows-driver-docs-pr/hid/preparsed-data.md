---
title: 预分析的数据
description: 预分析的数据
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- WDK HID 的已分析的数据
- WDK HID preparsed 的数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec1402e9c9deca3745b03476bb0eed4160ad7c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372962"
---
# <a name="preparsed-data"></a>预分析的数据





*Preparsed 数据*是报表描述符与关联的数据[顶级集合](top-level-collections.md)。 用户模式应用程序或内核模式驱动程序使用 preparsed 的数据而无需获取和解释设备的整个报表描述符提取特定的 HID 控件有关的信息。 在用户模式应用程序使用获取集合的 preparsed 的数据[ **HidD\_GetPreparsedData** ](https://msdn.microsoft.com/library/windows/hardware/ff539679)和内核模式驱动程序将使用[ **IOCTL\_HID\_获取\_集合\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541089)请求。

以下[HIDClass 支持例程](https://msdn.microsoft.com/library/windows/hardware/ff538865)支持提取和设置按钮和值数据：

[**HidP\_GetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539708)

[**HidP\_SetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539779)

[**HidP\_UnsetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539812)

[**HidP\_GetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539748)

[**HidP\_SetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539797)

[**HidP\_GetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539729)

[**HidP\_SetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539787)

[**HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)

[**HidP\_SetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539801)

 

 




