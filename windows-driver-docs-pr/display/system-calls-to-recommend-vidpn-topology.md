---
title: 用于建议 VidPN 拓扑的系统调用
description: 用于建议 VidPN 拓扑的系统调用
ms.assetid: cc23be93-be31-4069-960c-268a8b151063
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba2a559dabddfb1a65c13c207d29cbd57397c078
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829334"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>用于建议 VidPN 拓扑的系统调用


在运行 Windows 7 的计算机上，显示模式管理器（CALL CENTER.DMM）使用 CCD 数据库中的 VidPN 历史记录数据确定要应用的适当 VidPN 拓扑。 CALL CENTER.DMM 不再根据 Windows Vista 中的最后一个已知良好的拓扑确定 VidPN 拓扑。 因此，在 Windows 7 上，CALL CENTER.DMM 绝不会调用[**DxgkDdiRecommendVidPnTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)函数。

在 Windows Vista 及其 service pack 上，CALL CENTER.DMM 将继续调用*DxgkDdiRecommendVidPnTopology* ，请求驱动程序提供建议的功能 VidPN 拓扑。

 

 





