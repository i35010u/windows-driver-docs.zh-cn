---
title: NDIS 驱动程序的安全清单
description: NDIS 驱动程序的安全清单
ms.assetid: a7dee05d-6697-4061-a754-1d3854d7caea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d59de916eb42bbb232adc701dfbbf2f749a566d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566647"
---
# <a name="security-checklist-for-ndis-drivers"></a>NDIS 驱动程序的安全清单





若要确保您的驱动程序遵循良好安全做法，请执行以下操作：

-   如果可能，避免出于任何原因解析数据包有效负载信息的代码。 我们建议您删除任何此类代码，尤其是在处理卸载验证，从您的驱动程序的数据包处理调度例程。

-   检查您的驱动程序发送和接收的代码路径并仔细验证由于任何原因解析数据包有效负载信息的任何代码。

-   全面查看安全漏洞的驱动程序代码和发布该驱动程序之前测试您的驱动程序。 请务必验证错误的所有路径，以及正常代码路径。

-   运行随机数据包生成测试，以确保您的驱动程序可以抵御错误数据包信息。 将来，此类测试将是必需的设备徽标认证。

 

 





