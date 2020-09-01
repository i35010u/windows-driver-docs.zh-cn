---
title: 设计 WMI 微型端口驱动程序回调例程
description: 设计 WMI 微型端口驱动程序回调例程
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI SRBs WDK 存储，设计回调例程
- 回调例程 WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a51f8f1893b7c63c8099b52db799edc8cdca9db9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184705"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>设计 WMI 微型端口驱动程序回调例程


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


若要使用 SCSI 端口 WMI 库，必须在微型端口驱动程序中实现以下微型端口驱动程序回调例程：

[**HwScsiWmiExecuteMethod**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[**HwScsiWmiFunctionControl**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[**HwScsiWmiQueryDataBlock**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[**HwScsiWmiQueryReginfo**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[**HwScsiWmiSetDataBlock**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[**HwScsiWmiSetDataItem**](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)

以下部分将帮助你设计 *HwScsiWmiExecuteMethod* 回调例程和管理数据字段的回调例程：

[设计可以通过方法处理 WMI 类的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[设计可以通过数据字段处理 WMI 类的微型端口驱动程序回调例程](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

