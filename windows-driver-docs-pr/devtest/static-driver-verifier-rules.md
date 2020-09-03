---
title: DDI 合规性规则
description: DDI 合规性规则
ms.assetid: f020fff9-f880-4aa8-b422-5452728d2fdd
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 78c1e4ded33de3756c57efda227ba7529097687e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383881"
---
# <a name="ddi-compliance-rules"></a>DDI 合规性规则


本部分列出并介绍了可用于验证 Windows 驱动模型 (WDM) 、内核模式驱动程序框架 (KMDF) 、音频 (PortCls) 、AVStream (KS) 、NDIS 和 Storport 驱动程序的 Windows 设备驱动程序接口 (DDI) 符合性规则。 DDI 符合性规则定义了驱动程序和操作系统内核接口之间适当交互的要求。

[音频驱动程序的规则](rules-for-audio-drivers.md)  
[AVStream 驱动程序的规则](rules-for-avstream-drivers.md)  
[WDM 驱动程序的规则](sdv-rules-for-wdm-drivers.md)  
[KMDF 驱动程序的规则](sdv-rules-for-kmdf-drivers.md)  
[NDIS 驱动程序的规则](sdv-rules-for-ndis-drivers.md)  
[Storport 驱动程序的规则](sdv-rules-for-storport-drivers.md)  

### <a name="driver-verification-tools"></a>驱动程序验证工具

您可以使用 "代码分析工具"、" [静态驱动程序验证](./static-driver-verifier.md) 程序" 和 " [驱动程序验证](./driver-verifier.md) 程序" 来测试驱动程序是否符合 DDI 使用情况规则。 静态驱动程序验证器 (SDV) 对驱动程序源代码执行静态分析，因此你可以在开发周期的早期使用 SDV。 驱动程序验证程序与操作系统集成，因此你可以在生成、部署和安装驱动程序后，在运行时对其进行测试。

使用驱动程序源代码， [静态驱动程序验证](./static-driver-verifier.md) 器会创建驱动程序和操作系统的模型。 在此模型中，SDV 将驱动程序放置在一个敌意的环境中，并通过查找与)  ([静态驱动程序验证程序规则](./static-driver-verifier-rule.md) 的一组规范化的驱动程序符合性规则的冲突来测试代码路径。

从 Windows 8 开始，你可以将 [驱动程序验证程序](./driver-verifier.md) 配置为在已安装的驱动程序上运行一些相同的符合性检查，方法是启用 [DDI 相容性检查](./ddi-compliance-checking.md)。

## <a name="related-topics"></a>相关主题


[驱动程序验证程序](./driver-verifier.md) 
[静态驱动程序验证程序](./static-driver-verifier.md)
 

