---
title: 移动计划集成
description: 本主题介绍移动计划程序的集成步骤。
ms.assetid: F818B69D-DFA3-4296-B420-43F59D370E3C
keywords:
- Windows Mobile 计划集成，移动计划集成的移动运营商
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3c7fb09cf1195713a35843206dd5557bab689797
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845536"
---
# <a name="mobile-plans-integration"></a>移动计划集成

## <a name="overview"></a>概述

本主题介绍需要哪些步骤来集成和验证计划移动解决方案的移动运营商实现。

## <a name="mobile-plans-service-environments"></a>移动计划服务环境

有两个计划移动服务环境*过渡*并*生产*。 将中执行集成和验证*暂存*环境中，虽然*生产*环境仅用于商业启动。

## <a name="validation"></a>验证

本部分介绍测试和验证以确保已准备好将移到集成阶段必须执行的操作。

### <a name="mobile-operator-web-portal"></a>移动运营商的 web 门户

验证你可以运行 50 个端到端用户事例中定义的。 例如：

- Esim 卡配置文件安装。
- 激活热 SIM。
- 添加到你的订阅的余额。
- 正在取消事务。

### <a name="walled-garden"></a>围墙的花园

当用户没有余额，请确保用户可以访问 Walled Garden 站点中定义[Walled Garden](mobile-plans-device-experience.md#walled-garden)。

### <a name="getting-balance"></a>获取余额

1. Walled Garden 状态用户时，返回的余额必须为零。
2. 用户使用的数据，因为必须递减返回的平衡，以反映剩余的数据。
3. 为分配的时间内的超时期结束后`Create Order`调用 API，剩余的时间必须递减以反映剩余的时间。

### <a name="test-with-expired-mtls-certificate"></a>测试 MTLS 证书已过期

1. 如果没有 MTLS 证书验证 MO Api。 预期的状态：401 未经授权。
2. 验证 MTLS 证书已过期。 预期的状态：401 未经授权。

### <a name="getbalance-negative-tests"></a>GetBalance 反向测试

1. 验证使用无效 SIM。 预期的状态：404 找不到。
2. 验证未知的位置或错误的位置字符串/数字开头。 预期的状态：400 （错误请求）。
3. 验证筛选器限制为负数和超出 INT 的限制 预期的状态：400-错误的请求。 筛选器限制 （整数） 的预期状态 200 OK。
4. 验证调用`GetBalance`而无需任何*位置*（或空位置）， *fieldTemplate*，*限制*，和更多的组合的参数。 预期的状态：400 （错误请求） 与任何错误的参数值。 预期状态 200-OK。

### <a name="getbalance-api-load-test"></a>GetBalance API 负载测试

之前`GetBalance`API 启用在生产环境中，应测试计划移动服务和移动运营商服务以检查它们是否可以处理预计的负载。 移动运营商需要运行负载测试。 后已过，移动计划执行负载测试。 移动运营商应提供 1000 ICCIDs 暂时在负载测试中使用的列表。

此测试配置是从 10,000 Sim 的预计流量生成。 根据 3 次此流量投影计算峰值 RP。

- 将从 25 测试代理执行负载测试。
- 有关将执行负载测试：
  - 1000 个不同用户 (#ICCIDs) 使用 3 个 RP （峰值） 的 1 小时。
- 负载分布跨 Api 可能会按如下所示：

| API | 负载分布 | 预期的 RPS | 峰值 RPS |
| --- | --- | --- | --- |
| GetBalance | 96% | 1 | 3 |

在测试运行期间预期的成功率是：99.9%. 在获得此成功率，MO API 将准备好移动计划生产服务中启用。