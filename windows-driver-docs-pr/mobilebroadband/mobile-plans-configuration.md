---
title: 移动 Plans 配置
description: 本主题介绍移动计划程序的配置步骤。
ms.assetid: 95122BBB-0466-4130-9209-7EC6545DFD4D
keywords:
- Windows Mobile 计划配置中，移动计划配置移动操作员
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: a56ceca2d719f2813979c28b86b616b328f0425b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554750"
---
# <a name="mobile-plans-configuration"></a>移动 Plans 配置

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

本主题介绍如何在 Windows Mobile 计划支持的连接设备上构建基础。 它详细介绍了如何配置 esim 卡配置文件，以确保获得最佳使用者体验，以及如何提供可确保移动计划的服务配置信息正确呈现体验在 Windows 设备上。

## <a name="esim-profile-configuration-requirements"></a>esim 卡配置文件配置要求

你必须准备 esim 卡配置文件满足以下要求：

- Esim 卡配置文件不能锁定的 PIN。
- 必须从你 SM 中删除的 esim 卡配置文件-DP + 服务器直到接收确认配置文件下载已成功完成。 可重复使用的激活代码以重试下载相同的配置文件时下载此前在尝试已失败。 
- Esim 卡配置文件不能"不删除"执行停用"策略设置。
- 激活代码不能包含任何前缀如"LPA:"。
- MO 直接流后立即提供了该激活代码。
- Esim 卡配置文件可以立即从下载 SMDP + 服务器后 MO 直接流。
- 设备可以立即连接到网络的最终用户后下载 esim 卡并将其激活。

最后，移动计划用户体验需要的 esim 卡配置文件处于热状态，这意味着一个数据计划中激活实时下载 esim 卡配置文件之后。

## <a name="service-configuration"></a>服务配置

准备就绪后 esim 卡配置文件，需要配置服务平台，以支持您作为移动运营商 Microsoft 配置服务。 若要开始此过程，请发送电子邮件至[ DYNAMOpartnersup@microsoft.com ](mailto:swifipartnersup@microsoft.com)载入的以下信息： 

1.  想要用于你的产品的品牌名称。
2.  品牌徽标。 所需的解决方法如下所示：150 x 150、 188 x 188、 225 x 225、 600 x 600、 300x300 和 400x400 像素。 图像还应为完整出血以不透明。
3.  你的解决方案支持的国家/地区的列表。
4.  MO 直接门户 URI。
5.  通知 （在实现中所述） 的 URI。
6.  ICCID 范围或你想要想要将与移动计划相关联的范围。

下图显示了在计划移动应用中的商品信息和提供程序说明页 (PDP) 的布局示例。 "A"批注对应于该品牌徽标提交，和"B"批注与品牌名称相对应。

<img src="images/dynamo_configuration_mo_page.png" alt="Mobile Plans mobile operator page - asset usage example" title="移动计划移动运营商页-资产使用情况示例" width="600" />