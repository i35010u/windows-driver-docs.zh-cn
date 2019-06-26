---
title: 多功能设备限制
description: 多功能设备限制
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多功能音频设备 WDK，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a94fe1c2210cdf3800f08b7ed82cbe14ffc8188
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363223"
---
# <a name="multifunction-device-limits"></a>多功能设备限制


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


每个多功能设备的音频功能的数量受以下因素：

-   当适配器驱动程序调用[ **PcAddAdapterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddadapterdevice)，该函数的第四个参数*MaxObjects*，指定的最大数的微型端口驱动程序对象该驱动程序可以支持。 示例适配器驱动程序中 Microsoft Windows Driver Kit (WDK) 将此参数设置为最大的整数常量\_微型端口，通常定义为较小的值 （五个或更少）。 您可能需要增加此值，如果您计划支持多个立体声对或其他类型的子音频设备。

 

 




