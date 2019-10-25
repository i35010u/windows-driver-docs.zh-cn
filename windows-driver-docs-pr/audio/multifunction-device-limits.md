---
title: 多功能设备限制
description: 多功能设备限制
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多功能音频设备 WDK，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc780ab2bd7c1684c0d520747e9977b9708217de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832568"
---
# <a name="multifunction-device-limits"></a>多功能设备限制


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


每个多功能设备的音频功能数受以下因素限制：

-   当适配器驱动程序调用[**PcAddAdapterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)时，该函数的第四个参数*MaxObjects*指定该驱动程序可以支持的最大微型端口驱动程序对象数。 Microsoft Windows 驱动程序工具包（WDK）中的示例适配器驱动程序将此参数设置为整数常量 MAX\_微型端口，这通常定义为一个较小的值（5个或更少）。 如果计划支持多个立体声对或其他类型的音频 subdevices，则可能需要增加此值。

 

 




