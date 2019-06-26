---
title: 设计 WMI 微型端口驱动程序回调例程
description: 设计 WMI 微型端口驱动程序回调例程
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI Srb WDK 存储，设计回调例程
- 回调例程 WDK WMI Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4c778abfebf2989516a8ff2b0ea7611aa56145a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368297"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>设计 WMI 微型端口驱动程序回调例程


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


若要使用 SCSI 端口 WMI 库，必须在您的微型端口驱动程序中实现以下微型端口驱动程序回调例程：

[**HwScsiWmiExecuteMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[**HwScsiWmiFunctionControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[**HwScsiWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[**HwScsiWmiQueryReginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[**HwScsiWmiSetDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[**HwScsiWmiSetDataItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)

以下部分将帮助你设计*HwScsiWmiExecuteMethod*回调例程和管理数据字段的回调例程：

[设计处理 WMI 类的方法的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[设计处理 WMI 类的数据字段的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

 




