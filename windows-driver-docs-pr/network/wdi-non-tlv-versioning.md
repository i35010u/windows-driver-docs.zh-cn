---
title: WDI 非 TLV 版本控制
description: 本部分介绍 WDI 非 TLV 版本控制
ms.assetid: 19B5BEE1-BE17-40E3-99FA-D9BF4492D020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e4781e32ec0f4c24b068bc5b689ea65d64627a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842914"
---
# <a name="wdi-non-tlv-versioning"></a>WDI 非 TLV 版本控制


在 WDI 和 IHV 微型端口之间传递并包含[**ndis\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)的数据结构（如[**NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)）遵循标准 NDIS版本控制模型。 小型端口必须检查**修订**和**大小**字段，以确保它所关心的字段存在，并忽略任何额外的字段或数据而不会出错。 确保未排除较新版本或更大的此类结构。

不带[**NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)的所有数据结构（如[**WDI\_帧\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)）遵循 TLV 版本控制模型，其中 WDI 和微型端口使用由最低 WdiVersion 确定的大小/修订号ndis 中的值[ **\_WDI\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)和[**NDIS\_微型端口\_驱动程序\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)。

例如，如果 WDI 在 Ndis 中设置**WdiVersion** [ **\_WDI\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)设置为**WDI\_版本\_1\_0**，并在 [**NDIS\_微型端口设置 WdiVersion\_DRIVER\_WDI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics) **WDI\_版本\_2\_0**，则 WDI 和微型端口应使用与**WDI\_版本\_1 兼容的结构大小和定义**对于没有[**NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)字段的所有结构，\_0。 但是，在同一情况下，如果结构具有**NDIS\_对象\_标头**字段，WDI 和**小小**程序可以使用更大或更高的结构，前提是正确设置了**修订**和大小字段。

 

 





