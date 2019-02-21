---
title: 移动计划
description: 移动计划
ms.assetid: AA432EAE-A89B-4C4C-9539-BC2763091055
keywords:
- Windows Mobile 计划移动运营商
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: e954b7a95e53fa41543a716085fabe0347334172
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523899"
---
# <a name="mobile-plans"></a>移动计划

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="introduction"></a>简介

移动计划是在 Windows 10，版本 1803年中的程序和更高版本，可使移动运营商 (MOs) 和其他服务提供商向最终用户销售计划。 移动计划是以前的数据市场程序的新名称并不是单独或竞争的程序。

移动计划使最终用户能够执行以下操作：

- 安装并激活 esim 卡配置文件。
- 激活的设备上具有预付 (PAYG) 或流失的计划的移动运营商订阅。
- 顶级向上预付订阅时从数据和唯一可用的连接是移动连接。

## <a name="definition-of-terms"></a>术语的定义

| 术语 | 描述 |
| --- | --- |
| Contoso 移动电话 | 为了说明与解释这些主题中使用虚构移动运算符。 |
| COSA 数据库 | 国家/地区和运算符设置资产。 这是包含在 Windows 设备中使用的移动运营商的连接设置的数据库。 有关 COSA 的详细信息，请参阅[COSA 概述](cosa-overview.md)。 |
| 移动计划 | 此项目的名称。 |   
| 计划移动应用 | 若要启用移动计划，以前称为付费 Wi-fi 和移动电话 (PWC) 应用的 Microsoft 应用。 |
| PAYG | 现用现付 |
| RPS | 每秒请求数 |

## <a name="project-overview"></a>项目概述

移动计划项目集成组成四个阶段，其中每个高级任务。 其中一些高级任务适用于移动运营商，而有些则是联合的任务与移动运算符结合使用 Microsoft 适用的位置。 下图演示了移动计划项目的四个阶段。

<img src="images/dynamo_project_overview.png" alt="Mobile Plans project overview" title="移动计划项目概述" width="600" />

## <a name="functional-overview"></a>功能概述

下图显示了 Windows 10 设备如何使用移动计划与不同的服务和解决方案，以成功激活订阅并安装 esim 卡配置文件进行交互的高级视图。

下表描述关系图的每个组件。

| Component | 描述 |
| --- | --- |
| Windows 10 设备 | 支持 esim 卡的"始终连接 PC"运行 Windows 10 的最新版本。 |
| Microsoft Mobile 计划服务 | 服务终结点负责解决电话号码查询并提供移动运营商的信息，如月 web 门户 URL 和视觉对象资产，到 Windows 10 设备。 |
| 移动计划 Web API 和 Web 门户 | 负责托管的 web 服务 API 和 web 门户，允许 Windows 10 设备访问移动计划移动运营商网络中的终结点体验。 |
| SMDP + 服务器 | 负责创建、 生成，以及管理属于移动运营商的 esim 卡配置文件。 |

<img src="images/dynamo_functional_overview.png" alt="Mobile Plans functional overview" title="移动计划功能概述" width="600" />

上面的关系图的典型功能流如下所示：

1. Windows 10 设备上运行的计划移动应用解决计划移动服务中的电话号码查询。
2. 计划移动应用访问计划移动服务以检索月特定的信息。
3. 计划移动应用启动 MO web 门户，并将相关参数传递到 MO 门户。
4. 移动运营商的 esim 卡配置文件请求从 SM-DP + 服务器。 Esim 卡激活代码返回到移动计划移动运营商服务器。
5. 控件返回之后移动计划应用到 Windows 10 设备上，向 Windows 设备提供 esim 卡激活代码。
6. 在 Windows 10 设备使用的激活代码，并联系 SM-DP + 服务器检索的 esim 卡配置文件。 Esim 卡配置文件现在安装和激活 Windows 10 设备上。
7. 在 Windows 10 设备连接到移动运营商网络。

Windows 作为客户端使用计划移动应用，以使用移动计划的整体体验。 此应用程序联系 MO Web 门户，并会处理所有与之交互。 此外，一旦已返回的激活代码，计划移动应用程序负责进行下载、 安装和激活 esim 卡配置文件。

## <a name="get-started"></a>立即开始行动

若要开始使用计划流失移动体验，请执行以下步骤：

1. [配置](mobile-plans-configuration.md)
2. [实现](mobile-plans-implementation.md)
3. [集成](mobile-plans-integration.md)
4. [启动](mobile-plans-launch.md)

请参阅以下主题，获取有关移动计划的其他信息：

- [预付的体验](mobile-plans-prepaid-experience.md)
- [Appendix](mobile-plans-appendix.md)