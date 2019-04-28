---
title: 多功能设备限制
description: 多功能设备限制
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多功能音频设备 WDK，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbaf4bd034826c29e6dc126416d452a40df0c8d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332301"
---
# <a name="multifunction-device-limits"></a>多功能设备限制


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


每个多功能设备的音频功能的数量受以下因素：

-   当适配器驱动程序调用[ **PcAddAdapterDevice**](https://msdn.microsoft.com/library/windows/hardware/ff537683)，该函数的第四个参数*MaxObjects*，指定的最大数的微型端口驱动程序对象该驱动程序可以支持。 示例适配器驱动程序中 Microsoft Windows Driver Kit (WDK) 将此参数设置为最大的整数常量\_微型端口，通常定义为较小的值 （五个或更少）。 您可能需要增加此值，如果您计划支持多个立体声对或其他类型的子音频设备。

 

 




