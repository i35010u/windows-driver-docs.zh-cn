---
title: I2S 和 SCO 资源的管理
description: I2S 管理和 SCO 资源本主题将讨论中的 Windows 8.1 中的流式处理的蓝牙旁路音频此新支持设计所做的假设。
ms.assetid: C6CA73D9-0DCC-496D-8306-CB1625B86AC9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93401243ac280e5c5ff344f6f39e047fac7e3dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564906"
---
# <a name="management-of-i2s-and-sco-resources"></a>I2S 和 SCO 资源的管理


I2S 管理和 SCO 资源本主题将讨论中的 Windows 8.1 中的流式处理的蓝牙旁路音频此新支持设计所做的假设。

这一次 Windows 假定是只能有一个蓝牙主机控制器。 此外，HFP 同步连接方向 (SCO) 绕过支持假定只有一个绕过连接并且通过 HFP 设备驱动程序界面中，打开任何通道与该单个连接相关联。

音频驱动程序应将此通道进行仲裁和单跳过单个使用者按先来先处理的连接。 若要实现此目的的最简单方法是驱动程序以允许仅有单个筛选器来转换其插针，为获取状态。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[理论上的操作](theory-of-operation.md)  



