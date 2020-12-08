---
title: 测试有漏洞 NDIS 驱动程序所增加的成本
description: 测试有漏洞 NDIS 驱动程序所增加的成本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0411b503b99593fe660fb97f23d71b05408f0cfe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799433"
---
# <a name="added-costs-for-testing-vulnerable-ndis-drivers"></a>测试有漏洞 NDIS 驱动程序所增加的成本





建议从驱动程序的数据包处理调度例程中删除分析数据包有效负载的任何代码，特别是在处理卸载验证时。 若要自信此类代码，您必须对驱动程序进行广泛的测试，以确保安全且正确地处理所有潜在的错误条件。 这种测试意味着增加了测试成本。

微型端口驱动程序应避免分析数据包数据。 它们不应尝试处理硬件无法处理的卸载操作。 在系统的接收端，请特别注意驱动程序如何检查数据包负载信息。 驱动程序的发送端也可能会受到路由/桥接系统配置的影响。

 

 





