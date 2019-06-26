---
title: WDI 常规数据路径接口
description: 本部分介绍常规 WDI 数据路径接口
ms.assetid: 5B40171C-4E5F-4C35-A6E7-1EA5181C02E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e182e1c5515d2aca6d17f6ba6aee7d51f83d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387219"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 常规数据路径接口


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 帧处理和帧元数据


WDI 和形式的谈论之间传递 802.11 帧[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) (NBL) 链。 每个 NBL 表示一个 MSDU。 通过宏，NBL 结构提供了对数据缓冲区和对元数据，包括操作系统填充 Wi-fi TX 元数据的访问的操作。 结构是可扩展的通过其上下文和**MiniportReserved**成员。 **MiniportReserved\[0\]** 指向类型的缓冲区[ **WDI\_帧\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)。 此缓冲区分配由 WDI TX 路径中和通过回调 RX 路径中谈论[ *NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)。 谈论使用 MiniportReserved\[1\]来存储任何其他框架元数据。

## <a name="datapath-management-requests-and-indications"></a>数据路径管理请求和指示


数据路径管理请求和指示函数参考，请参阅[WDI 数据路径管理功能](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

## <a name="related-topics"></a>相关主题


[**NDIS\_WDI\_DATA\_API**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_wdi_data_api)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[*NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)

[**WDI\_FRAME\_METADATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)

 

 






