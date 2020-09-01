---
title: 错误注入
description: 错误注入
ms.assetid: d97d49bc-b216-40d6-afd1-aecff624624d
keywords:
- Windows 硬件错误体系结构 WDK，错误注入
- WHEA WDK，错误注入
- 硬件错误 WDK WHEA，错误注入
- 错误 WDK WHEA，错误注入
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误注入
- PSHED 插件 WDK WHEA，错误注入
- 错误注入 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80a2c1d11f882f5c67ae8c9bc7d9f435981aeb18
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213087"
---
# <a name="error-injection"></a>错误注入


PSHED 向操作系统公开一个接口，Windows 内核通过此接口可导致硬件错误事件发生，以便进行测试和验证。 如果实现了参与错误注入的 PSHED 插件，则 PSHED 会调用它来执行错误注入操作。

有关如何实现参与错误注入的 PSHED 插件的详细信息，请参阅 [参与错误注入](participating-in-error-injection.md)。

用户模式管理应用程序可以通过调用 [WHEA 管理 API](/windows-hardware/drivers/ddi/_whea/)，将错误注入硬件平台。 有关如何实现 WHEA 管理应用程序的详细信息，请参阅 [WHEA 管理应用程序](whea-management-applications.md)。

 

