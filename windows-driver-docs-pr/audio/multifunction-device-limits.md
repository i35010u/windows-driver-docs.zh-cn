---
title: 多功能设备限制
description: 多功能设备限制
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多功能音频设备 WDK，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29a17ab9c478347ee55a4cad302651492d7e3400
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210563"
---
# <a name="multifunction-device-limits"></a>多功能设备限制


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


每个多功能设备的音频功能数受以下因素限制：

-   当适配器驱动程序调用 [**PcAddAdapterDevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)时，该函数的第四个参数 *MaxObjects*指定该驱动程序可以支持的最大微型端口驱动程序对象数。 Microsoft Windows 驱动程序工具包中的示例适配器驱动程序 (WDK) 将此参数设置为整数常量 MAX \_ 微型端口，这通常定义为小数值 (5 个或更少) 。 如果计划支持多个立体声对或其他类型的音频 subdevices，则可能需要增加此值。

 

