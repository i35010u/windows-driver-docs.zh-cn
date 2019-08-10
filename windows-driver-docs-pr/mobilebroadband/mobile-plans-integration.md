---
title: 移动计划集成
description: 本主题介绍 Mobile plan 计划的集成步骤。
ms.assetid: F818B69D-DFA3-4296-B420-43F59D370E3C
keywords:
- Windows Mobile 计划集成, 移动计划集成移动运营商
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 882a5995c7558be761a0dca9974e2e7755c94897
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948038"
---
# <a name="mobile-plans-integration"></a>移动计划集成

## <a name="overview"></a>概述

本主题介绍集成和验证移动计划解决方案的移动运营商实现所需的步骤。

## <a name="mobile-plans-service-environments"></a>移动计划服务环境

有两个移动计划服务环境:*过渡*和*生产*。 集成和验证将在*过渡*环境中执行, 而*生产*环境仅用于商业发布。

## <a name="validation"></a>验证

本部分介绍你必须执行的测试和验证, 以确保你已准备好进入集成阶段。

### <a name="mobile-operator-web-portal"></a>移动运营商 web 门户

验证你是否可以运行你定义的50端到端用户案例。 例如：

- 安装 eSIM 配置文件。
- 激活热 SIM。
- 向订阅添加余额。
- 取消事务。

### <a name="walled-garden"></a>围墙花园

如果用户没有余额, 请确保用户可以访问[围墙园](mobile-plans-walled-garden.md)中定义的围墙园站点。

### <a name="getting-balance"></a>取得平衡

1. 当用户处于围墙园状态时, 返回的余额必须为零。
2. 用户使用数据时, 返回的余额必须递减, 以反映剩余的数据。
3. 在调用`Create Order` API 之后, 分配的时间就会发生, 剩余时间必须递减, 以反映剩余的时间。

### <a name="test-with-expired-mtls-certificate"></a>测试已过期的 MTLS 证书

1. 验证 MO Api, 但不要包含 MTLS 证书。 预期状态:401未授权。
2. 使用过期的 MTLS 证书进行验证。 预期状态:401未授权。

### <a name="getbalance-negative-tests"></a>GetBalance 否定性测试

1. 使用无效的 SIM 验证。 预期状态:找不到404。
2. 验证是否存在未知位置或错误位置字符串/编号。 预期状态:400 (错误的请求)。
3. 验证筛选器限制为负数, 超过 INT 的限制。 预期状态:400-请求错误。 对于筛选器限制 (整数), 应为状态 200 OK。
4. 在不使用任何`GetBalance` *位置*(或空位置)、 *fieldTemplate*、*限制*以及参数的更多组合的情况下, 验证对的调用。 预期状态:错误的参数值为 400 (错误的请求)。 预期状态200–正常。

### <a name="getbalance-api-load-test"></a>GetBalance API 负载测试

在生产环境中启用API之前,应测试移动计划服务和移动运营商服务,以查看它们能否处理预计的负载。`GetBalance` 移动运营商应运行负载测试。 完成后, 移动计划将执行负载测试。 移动运营商应提供在负载测试中使用暂时的 1000 Iccid 的列表。

此测试配置是通过 10000 Sim 的预计流量生成的。 峰值 RPS 根据此流量预测的3倍计算得出。

- 将从25个测试代理执行负载测试。
- 负载测试将为以下内容执行:
  - 1小时, 1000 具有3个不同用户 (#ICCIDs) 和3个 RPS (峰值)。
- 负载分布跨 Api 如下所示:

| API | 负载分配 | 预期 RPS | 最大 RPS |
| --- | --- | --- | --- |
| GetBalance | 96% | 1 | 3 |

在测试运行期间, 预期的成功率为:**99.9%** 和平均延迟:**400ms**。 达到此成功率后, MO API 就可以在移动计划生产服务中启用。
