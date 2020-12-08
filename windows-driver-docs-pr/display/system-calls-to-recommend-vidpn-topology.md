---
title: 用于建议 VidPN 拓扑的系统调用
description: 用于建议 VidPN 拓扑的系统调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5130ebee3882cc50c3cd5bce7de43f1db9f20925
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839571"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>用于建议 VidPN 拓扑的系统调用


在运行 Windows 7 的计算机上， (CALL CENTER.DMM 的显示模式管理器) 确定要使用 CCD 数据库中的 VidPN 历史记录数据应用的适当 VidPN 拓扑。 CALL CENTER.DMM 不再根据 Windows Vista 中的最后一个已知良好的拓扑确定 VidPN 拓扑。 因此，在 Windows 7 上，CALL CENTER.DMM 绝不会调用 [**DxgkDdiRecommendVidPnTopology**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology) 函数。

在 Windows Vista 及其 service pack 上，CALL CENTER.DMM 将继续调用 *DxgkDdiRecommendVidPnTopology* ，请求驱动程序提供建议的功能 VidPN 拓扑。

 

