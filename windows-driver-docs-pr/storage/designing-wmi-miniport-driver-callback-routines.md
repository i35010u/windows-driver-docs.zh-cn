---
title: 设计 WMI 微型端口驱动程序回调例程
description: 设计 WMI 微型端口驱动程序回调例程
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI SRBs WDK 存储，设计回调例程
- 回调例程 WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7678735735af3ef98f64573a819fc2e0c399e89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845182"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>设计 WMI 微型端口驱动程序回调例程


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


若要使用 SCSI 端口 WMI 库，必须在微型端口驱动程序中实现以下微型端口驱动程序回调例程：

[**HwScsiWmiExecuteMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[**HwScsiWmiFunctionControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[**HwScsiWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[**HwScsiWmiQueryReginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[**HwScsiWmiSetDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[**HwScsiWmiSetDataItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)

以下部分将帮助你设计*HwScsiWmiExecuteMethod*回调例程和管理数据字段的回调例程：

[设计使用方法处理 WMI 类的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[设计使用数据字段处理 WMI 类的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

 




