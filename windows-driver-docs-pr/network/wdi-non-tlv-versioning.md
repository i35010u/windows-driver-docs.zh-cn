---
title: WDI 非 TLV 版本控制
description: 本部分介绍 WDI 非 TLV 版本控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3440956ea6c7b23f4a97ffe92b3ad7fc8c1ca09
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248483"
---
# <a name="wdi-non-tlv-versioning"></a>WDI 非 TLV 版本控制


在 WDI 和 IHV 微型端口之间传递并包含 [**ndis \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header) 的数据结构 (如 [**ndis \_ 微型端口 \_ 驱动程序 \_ WDI \_ 特征**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)) 遵循标准的 ndis 版本控制模型。 小型端口必须检查 **修订** 和 **大小** 字段，以确保它所关心的字段存在，并忽略任何额外的字段或数据而不会出错。 确保未排除较新版本或更大的此类结构。

不带 [**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header)的所有数据结构 (如 [**WDI \_ 帧 \_ 元数据**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)) 遵循 TLV 版本控制模型，其中 WDI 和微型端口使用由 [**ndis \_ WDI \_ INIT \_ 参数**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)和 [**ndis \_ 微型端口 \_ 驱动程序 \_ WDI \_ 特征**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)中的最小 **WdiVersion** 值决定的大小/修订。

例如，如果 WDI 在 [**ndis \_ WDI \_ INIT \_ 参数**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)中将 **WdiVersion** 设置为 **WDI \_ 版本 \_ 1 \_ 0**，而微型端口将 [**ndis \_ 微型端口 \_ 驱动程序 \_ WdiVersion \_ 特征**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)中的 " **WDI** " 设置为 **WDI \_ 版本 \_ 2 \_ 0**，则对于不带 [**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header)字段的所有结构，WDI 和微型端口都应使用与 **WDI \_ 版本 \_ 1 \_ 0** 兼容的结构大小和定义。 但是，在同一情况下，如果结构具有 **NDIS \_ 对象 \_ 标头** 字段，则 WDI 和微型端口可以使用更大或更高的结构，只要正确设置了 **修订** 和 **大小** 字段。

 

