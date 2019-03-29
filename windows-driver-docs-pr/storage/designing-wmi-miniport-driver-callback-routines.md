---
title: 设计 WMI 微型端口驱动程序回调例程
description: 设计 WMI 微型端口驱动程序回调例程
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI Srb WDK 存储，设计回调例程
- 回调例程 WDK WMI Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80e519a45d54adc5fe7f320593c4112c17a97b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577291"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>设计 WMI 微型端口驱动程序回调例程


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


若要使用 SCSI 端口 WMI 库，必须在您的微型端口驱动程序中实现以下微型端口驱动程序回调例程：

[**HwScsiWmiExecuteMethod**](https://msdn.microsoft.com/library/windows/hardware/ff557332)

[**HwScsiWmiFunctionControl**](https://msdn.microsoft.com/library/windows/hardware/ff557338)

[**HwScsiWmiQueryDataBlock**](https://msdn.microsoft.com/library/windows/hardware/ff557340)

[**HwScsiWmiQueryReginfo**](https://msdn.microsoft.com/library/windows/hardware/ff557344)

[**HwScsiWmiSetDataBlock**](https://msdn.microsoft.com/library/windows/hardware/ff557349)

[**HwScsiWmiSetDataItem**](https://msdn.microsoft.com/library/windows/hardware/ff557357)

以下部分将帮助你设计*HwScsiWmiExecuteMethod*回调例程和管理数据字段的回调例程：

[设计处理 WMI 类的方法的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[设计处理 WMI 类的数据字段的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

 




