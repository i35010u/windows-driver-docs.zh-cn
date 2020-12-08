---
title: NDIS 驱动程序的安全清单
description: NDIS 驱动程序的安全清单
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dd0e506eacfa36bfd36feaa5abf3c7d4c7653e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815889"
---
# <a name="security-checklist-for-ndis-drivers"></a>NDIS 驱动程序的安全清单





若要确保您的驱动程序遵循良好的安全做法，请执行以下操作：

-   如果可能，请避免出于任何原因分析数据包有效负载信息的代码。 建议从驱动程序的数据包处理调度例程中删除任何此类代码，特别是处理卸载验证。

-   检查驱动程序的发送和接收代码路径，并仔细验证是否有任何代码分析了数据包有效负载信息，因为任何原因。

-   在释放驱动程序之前，请仔细查看安全漏洞的驱动程序代码并测试驱动程序。 请确保验证所有错误路径以及正常的代码路径。

-   运行随机数据包生成测试，以确保驱动程序可以抵御损坏的数据包信息。 将来，此类测试是设备徽标认证所必需的。

 

 





