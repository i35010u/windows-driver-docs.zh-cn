---
title: WDI 常规数据路径接口
description: 本部分介绍常规 WDI 数据路径接口
ms.assetid: 5B40171C-4E5F-4C35-A6E7-1EA5181C02E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5253cf0535a14bbcf828cf851646f75e20abf97a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842930"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 常规数据路径接口


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 帧处理和帧元数据


802.11 帧是在 WDI 和 TAL 之间以[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)（NBL）链的形式传递的。 每个 NBL 都表示一个 MSDU。 通过宏，NBL 结构提供对数据缓冲区的操作和对元数据的访问，包括操作系统填充的 Wi-fi TX 元数据。 结构可通过其上下文和**MiniportReserved**成员进行扩展。 **MiniportReserved\[0\]** 指向[**WDI 类型\_帧\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)的缓冲区。 此缓冲区由 WDI 在 TX 路径中分配，由 RX 路径中的 TAL 通过回调[*NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)分配。 TAL 使用 MiniportReserved\[1\] 来存储任何其他框架元数据。

## <a name="datapath-management-requests-and-indications"></a>数据路径管理请求和指示


有关数据路径管理请求和指示函数引用，请参阅[WDI 数据路径管理功能](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

## <a name="related-topics"></a>相关主题


[**NDIS\_WDI\_数据\_API**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_data_api)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[*NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)

[**WDI\_\_元数据框架**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)

 

 






