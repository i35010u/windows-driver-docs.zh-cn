---
title: 测试有漏洞 NDIS 驱动程序所增加的成本
description: 测试有漏洞 NDIS 驱动程序所增加的成本
ms.assetid: ee748650-92e6-4885-895e-c030cf33f315
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1862e368e5d07f16822cc85a71e8339461609649
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367789"
---
# <a name="added-costs-for-testing-vulnerable-ndis-drivers"></a>测试有漏洞 NDIS 驱动程序所增加的成本





我们建议您删除解析数据包有效负载，尤其是在处理卸载验证，从您的驱动程序的数据包处理调度例程的任何代码。 若要让置信度在此类代码，需要进行广泛的测试驱动程序以确保安全地且正确地处理所有潜在的错误条件。 这种测试方式增加测试成本。

微型端口驱动程序应避免分析数据包数据。 它们不应尝试处理无法处理硬件的卸载操作。 在系统的接收方，要特别注意您的驱动程序如何检查数据包有效负载信息。 此外可能会在发送端的驱动程序可能会影响路由/桥接系统配置。

 

 





