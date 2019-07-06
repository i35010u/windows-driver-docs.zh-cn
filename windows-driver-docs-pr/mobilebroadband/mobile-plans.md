---
title: 移动计划概述
description: 移动计划概述
ms.assetid: AA432EAE-A89B-4C4C-9539-BC2763091055
keywords:
- Windows Mobile 计划移动运营商
ms.author: windowsdriverdev
ms.date: 07/05/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: f67b41b18cbd12b7583261fc4307f2dbeffeb257
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608504"
---
# <a name="mobile-plans-overview"></a>移动计划概述

## <a name="introduction"></a>简介

移动计划是在 Windows 10，版本 1803年中的程序和更高版本，可使移动运营商 (MOs) 和其他服务提供商向最终用户销售计划。

移动计划使最终用户能够执行以下操作：

- 安装并激活 esim 卡配置文件。
- 激活的设备上具有预付 (PAYG) 或流失的计划的移动运营商订阅。
- 顶级的订阅时从数据和唯一可用的连接是移动连接。

## <a name="definition-of-terms"></a>术语的定义

| 术语 | 描述 |
| --- | --- |
| Contoso 移动电话 | 为了说明与解释这些主题中使用虚构移动运算符。 |
| COSA 数据库 | 国家/地区和运算符设置资产。 这是包含在 Windows 设备中使用的移动运营商的连接设置的数据库。 有关 COSA 的详细信息，请参阅[COSA 概述](cosa-overview.md)。 |
| 移动套餐 | 此项目的名称。 |
| 计划移动应用 | 若要启用 Windows 10 设备上的移动计划的 Microsoft 应用。 |
| 计划移动服务 | 云服务，使移动计划解决方案。 |
| RPS | 每秒请求数。 |

## <a name="project-overview"></a>项目概述

移动计划项目集成组成四个阶段，其中每个[高级别任务](mobile-plans-appendix.md#high-level-integration-schedule)。 其中一些高级任务适用于移动运营商，而有些则是联合的任务与移动运算符结合使用 Microsoft 适用的位置。

| 阶段 | 描述 |
| --- | --- |
| **Feasiblity** | 移动运营商评估计划移动解决方案、 摘要本文档中，并访问其 Microsoft 代表的问题提供根据需要。 |
| **实现** | 移动运营商开发他们根据其用户用例和请求移动计划配置和所需的 Windows 配置的解决方案。 |
| **集成** | 中移动计划以运行端到端验证启用了移动运营商。 |
| **启动** | 通过移动计划上市商业上启动移动运营商。 |

## <a name="functional-overview"></a>功能概述

下图显示了 Windows 10 设备如何使用移动计划与不同的服务和解决方案，以成功激活订阅并安装 esim 卡配置文件进行交互的高级视图。

下表描述关系图的每个组件。

| 组件 | 描述 |
| --- | --- |
| Windows 10 设备 | 支持 esim 卡的"始终连接 PC"运行 Windows 10 的最新版本。 |
| Microsoft Mobile 计划服务 | 服务终结点负责提供移动运营商的信息，如月 web 门户 URL 和视觉对象资产，到 Windows 10 设备。 |
| 移动计划 Web API 和 Web 门户 | 负责托管的 web 服务 API 和 web 门户，允许 Windows 10 设备访问移动计划移动运营商网络中的终结点体验。 |
| SM-DP + 服务器 | 负责创建、 生成，以及管理属于移动运营商的 esim 卡配置文件。 |

<img src="images/mobile_plans_functional_overview.png" alt="Mobile Plans functional overview" title="移动计划功能概述" width="400" />

上面的关系图的典型功能流如下所示：

1. 计划移动应用在 Windows 10 设备上启动，并从移动计划服务检索基本功能的信息。
   - 计划移动应用访问计划移动服务以检索月特定的信息。
2. 计划移动应用启动 MO Web 门户，并将相关参数传递到 MO 门户。
3. 移动运营商的 esim 卡配置文件请求从 SM-DP + 服务器。 Esim 卡激活代码返回到移动计划移动运营商 web 门户。
4. 控件返回之后移动计划应用到 Windows 10 设备上，向 Windows 设备提供 esim 卡激活代码。
5. 在 Windows 10 设备使用的激活代码，并联系 SM-DP + 服务器检索的 esim 卡配置文件。 Esim 卡配置文件现在安装和激活 Windows 10 设备上。
6. 在 Windows 10 设备连接到移动运营商网络。

Windows 作为客户端使用计划移动应用，以使用移动计划的整体体验。 此应用程序联系 MO Web 门户，并会处理所有与之交互。 此外，一旦已返回的激活代码，计划移动应用程序负责进行下载、 安装和激活 esim 卡配置文件。

## <a name="get-started"></a>立即开始行动

若要开始使用移动计划体验，请联系 Microsoft 代表联系以讨论项目实现。 请按照下列步骤以了解技术详细信息中的解决方案的指南。

1. [移动运营商用例](mobile-plans-use-cases.md)
2. [集成](mobile-plans-integration.md)
3. [启动](mobile-plans-launch.md)

请参阅以下主题，获取有关移动计划的其他信息：

- [附录](mobile-plans-appendix.md)