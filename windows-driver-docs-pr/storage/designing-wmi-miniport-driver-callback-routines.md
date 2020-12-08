---
title: 设计 WMI 微型端口驱动程序回调例程
description: 设计 WMI 微型端口驱动程序回调例程
keywords:
- WMI SRBs WDK 存储，设计回调例程
- 回调例程 WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bffea89cbc34a0dfbf76f41ca84cde4123b38aae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804689"
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

 

