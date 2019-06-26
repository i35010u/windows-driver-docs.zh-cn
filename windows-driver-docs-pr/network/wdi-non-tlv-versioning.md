---
title: WDI 非 TLV 版本控制
description: 本部分介绍 WDI 非 TLV 版本控制
ms.assetid: 19B5BEE1-BE17-40E3-99FA-D9BF4492D020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bc4495562384a904e542575e85e66fdc59c1f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381153"
---
# <a name="wdi-non-tlv-versioning"></a>WDI 非 TLV 版本控制


WDI 和 IHV 微型端口之间传递，并且包含的数据结构[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header) (如[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)) 遵循标准的 NDIS 版本控制模型。 微型端口必须检查**修订**并**大小**字段以确保它所关注的字段不存在，并忽略任何额外字段或数据不会出错。 请确保未排除较新修订或此类结构的更大的大小。

所有数据结构，无需[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header) (如[ **WDI\_帧\_的元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_frame_metadata))，请按 TLV 版本控制模式，其中 WDI 和微型端口使用由最小大小/修订**WdiVersion**值从[ **NDIS\_WDI\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)并[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics).

例如，如果设置 WDI **WdiVersion**中[ **NDIS\_WDI\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)到**WDI\_版本\_1\_0**，以及的微型端口集**WdiVersion**中[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)到**WDI\_版本\_2\_0**，则应使用的结构大小 WDI 和微型端口和定义与兼容**WDI\_版本\_1\_0**的所有结构，无需[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)字段。 但是，在这种情况，但与结构都**NDIS\_对象\_标头**字段、 WDI 和微型端口可能会使用长达一个更大或更高版本结构**修订**并**大小**字段是否正确设置。

 

 





