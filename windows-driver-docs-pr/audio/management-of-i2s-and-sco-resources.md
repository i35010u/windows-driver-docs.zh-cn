---
title: I2S 和 SCO 资源的管理
description: I2S 和 SCO 资源的管理主题讨论了在为 Windows 8.1 中的蓝牙绕过音频流设计设计时所做的假设。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95d4e3d085903015158b00aa900e6885f8f79fd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801037"
---
# <a name="management-of-i2s-and-sco-resources"></a>I2S 和 SCO 资源的管理


I2S 和 SCO 资源的管理主题讨论了在为 Windows 8.1 中的蓝牙绕过音频流设计设计时所做的假设。

目前，Windows 假定只有一个蓝牙主机控制器。 而且，HFP 同步连接 (SCO) 绕过支持假定只有一个绕过连接，并且通过 HFP 设备驱动程序接口打开的任何通道均与该单一连接关联。

音频驱动程序应该根据第一方服务的原则，为单个使用者仲裁此通道和单个绕过连接。 实现此目的的最简单方法是让驱动程序仅允许单个筛选器将其 pin 转换为获取状态。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[操作理论](theory-of-operation.md)  



