---
title: WDI 常规数据路径接口
description: 本部分介绍常规 WDI 数据路径接口
ms.assetid: 5B40171C-4E5F-4C35-A6E7-1EA5181C02E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d12c26e570cd869624a354e4e1247d68c8f193d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367505"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 常规数据路径接口


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 帧处理和帧元数据


WDI 和形式的谈论之间传递 802.11 帧[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388) (NBL) 链。 每个 NBL 表示一个 MSDU。 通过宏，NBL 结构提供了对数据缓冲区和对元数据，包括操作系统填充 Wi-fi TX 元数据的访问的操作。 结构是可扩展的通过其上下文和**MiniportReserved**成员。 **MiniportReserved\[0\]** 指向类型的缓冲区[ **WDI\_帧\_元数据**](https://msdn.microsoft.com/library/windows/hardware/dn897827)。 此缓冲区分配由 WDI TX 路径中和通过回调 RX 路径中谈论[ *NdisWdiAllocateWiFiFrameMetaData*](https://msdn.microsoft.com/library/windows/hardware/mt297597)。 谈论使用 MiniportReserved\[1\]来存储任何其他框架元数据。

## <a name="datapath-management-requests-and-indications"></a>数据路径管理请求和指示


数据路径管理请求和指示函数参考，请参阅[WDI 数据路径管理功能](https://msdn.microsoft.com/library/windows/hardware/mt297634)。

## <a name="related-topics"></a>相关主题


[**NDIS\_WDI\_DATA\_API**](https://msdn.microsoft.com/library/windows/hardware/mt297620)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[*NdisWdiAllocateWiFiFrameMetaData*](https://msdn.microsoft.com/library/windows/hardware/mt297597)

[**WDI\_FRAME\_METADATA**](https://msdn.microsoft.com/library/windows/hardware/dn897827)

 

 






