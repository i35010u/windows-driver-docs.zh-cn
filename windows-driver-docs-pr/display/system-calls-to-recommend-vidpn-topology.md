---
title: 用于建议 VidPN 拓扑的系统调用
description: 用于建议 VidPN 拓扑的系统调用
ms.assetid: cc23be93-be31-4069-960c-268a8b151063
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2d6b33b223c0549e64965ff471e50b102844193
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352847"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>用于建议 VidPN 拓扑的系统调用


在运行 Windows 7 的计算机，显示模式下管理器 (DMM) 确定要应用 CCD 数据库中使用 VidPN 历史记录数据的适当 VidPN 拓扑。 DMM 无法再确定 VidPN 拓扑像在 Windows Vista 中基于上次已知良好的拓扑。 因此，在 Windows 7 DMM 永远不会调用[ **DxgkDdiRecommendVidPnTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff559782)函数。

继续在 Windows Vista 以及其服务包，调用 DMM *DxgkDdiRecommendVidPnTopology*请求该驱动程序提供的建议功能 VidPN 拓扑。

 

 





