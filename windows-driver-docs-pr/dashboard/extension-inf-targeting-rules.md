---
title: 已定义的扩展 INF 目标评估规则
description: 策略定义将扩展 INF 作为目标的方式
ms.topic: article
ms.date: 09/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 11193410719347b8cb05a0c92fbc23fd20b26265
ms.sourcegitcommit: 068a9875851a278935078ba7f1ab65a3bb37235c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92100646"
---
# <a name="extension-inf-targeting-evaluation-rules-defined"></a>已定义的扩展 INF 目标评估规则

在朝着正确组件化新式驱动程序发展的过程中，我们将分享一些关于如何评估这些不断发展的驱动程序的计划。 

请记住驱动程序组件化背后的基础原则： 

>- 基本驱动程序旨在提供核心设备功能，可以面向广泛的受众。
> 
>- 扩展驱动程序通常旨在提供系统特定的自定义内容，必须面向特定受众。  最佳做法是，INF 应仅针对单个 OEM。 为了进行策略检查和验证，我们重点关注你选择发布的 HWID。 目标应只包括 HWID 和 CHID，它们是由扩展 INF 专门自定义的且仅限于单个 OEM。 
> 
>- 如果在 INF 中引用了多个 OEM 的 HWID，则在发布到列出的每个 HWID 时使用 CHID 将不会构成特定的目标。 此做法将无法通过策略检查。 

下面介绍在 Driver Shiproom 中处理提交内容时如何评估这些原则：

  **扩展 INF 是否针对没有 CHID 的 2-ID？**
  
  如果是：拒绝。 扩展 INF 受众并不广泛。

  **扩展 INF 是否针对跨多个 OEM 的系统？（根据 CHID 和 HWID 分析）**
  
  如果是：拒绝。 扩展 INF 不针对跨多个 OEM 的系统，因为它们应专门针对 OEM 系统。

  **扩展 INF 是否缺少声明性基类？**
  
  如果是：拒绝。 扩展 INF 仅与 DCH 驱动程序兼容。 此规则的唯一例外是，扩展 INF 与收件箱驱动程序匹配（例如，对于固件更新方案或 HSA 方案）。 

如果你对这些规则有任何疑问或反馈，请告诉我们。
