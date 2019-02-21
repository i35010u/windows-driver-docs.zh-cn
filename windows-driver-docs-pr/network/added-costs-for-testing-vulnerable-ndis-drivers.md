---
title: 用于测试的易受攻击的 NDIS 驱动程序添加了的成本
description: 用于测试的易受攻击的 NDIS 驱动程序添加了的成本
ms.assetid: ee748650-92e6-4885-895e-c030cf33f315
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1862e368e5d07f16822cc85a71e8339461609649
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542202"
---
# <a name="added-costs-for-testing-vulnerable-ndis-drivers"></a>用于测试的易受攻击的 NDIS 驱动程序添加了的成本





我们建议您删除解析数据包有效负载，尤其是在处理卸载验证，从您的驱动程序的数据包处理调度例程的任何代码。 若要让置信度在此类代码，需要进行广泛的测试驱动程序以确保安全地且正确地处理所有潜在的错误条件。 这种测试方式增加测试成本。

微型端口驱动程序应避免分析数据包数据。 它们不应尝试处理无法处理硬件的卸载操作。 在系统的接收方，要特别注意您的驱动程序如何检查数据包有效负载信息。 此外可能会在发送端的驱动程序可能会影响路由/桥接系统配置。

 

 





