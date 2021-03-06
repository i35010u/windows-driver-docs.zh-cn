---
title: WDI 常规数据路径接口
description: 本部分介绍常规 WDI 数据路径接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7b32e06e9888097cba2f836cc1c08cd817dd71b
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247791"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 常规数据路径接口


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 帧处理和帧元数据


802.11 帧在 WDI 和 TAL 之间以 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 的形式传递 (NBL) 链。 每个 NBL 都表示一个 MSDU。 通过宏，NBL 结构提供对数据缓冲区的操作和元数据的访问，包括 Wi-Fi TX 元数据填充的操作系统。 结构可通过其上下文和 **MiniportReserved** 成员进行扩展。 **MiniportReserved \[ 0 \]** 指向 [**WDI \_ 帧 \_ 元数据**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)类型的缓冲区。 此缓冲区由 WDI 在 TX 路径中分配，由 RX 路径中的 TAL 通过回调 [*NdisWdiAllocateWiFiFrameMetaData*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)分配。 TAL 使用 MiniportReserved \[ 1 \] 存储任何其他框架元数据。

## <a name="datapath-management-requests-and-indications"></a>数据路径管理请求和指示


有关数据路径管理请求和指示函数引用，请参阅 [WDI 数据路径管理功能](/windows-hardware/drivers/ddi/_netvista/)。

## <a name="related-topics"></a>相关主题


[**NDIS \_ WDI \_ 数据 \_ API**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_data_api)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)

[*NdisWdiAllocateWiFiFrameMetaData*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)

[**WDI \_ 框架 \_ 元数据**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)

 

