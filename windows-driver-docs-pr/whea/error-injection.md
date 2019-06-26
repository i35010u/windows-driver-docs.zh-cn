---
title: 错误注入
description: 错误注入
ms.assetid: d97d49bc-b216-40d6-afd1-aecff624624d
keywords:
- Windows 硬件错误体系结构 WDK，错误注入
- WHEA WDK，错误注入
- 硬件错误 WDK WHEA，错误注入
- 错误 WDK WHEA，错误注入
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误注入
- PSHED 插件 WDK WHEA 错误注入
- 错误注入 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64d400dc40faa373e0cd3c25f58898451d9b95e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362597"
---
# <a name="error-injection"></a>错误注入


PSHED 公开一个接口对通过该 Windows 内核可能导致硬件错误事件，以进行测试和验证的操作系统。 如果 PSHED 插件实现参与错误注入，它是然后调用 PSHED 执行错误注入操作。

有关如何在错误注入实现参与 PSHED 插件的详细信息，请参阅[参与错误注入](participating-in-error-injection.md)。

用户模式下管理应用程序可以通过调用到硬件平台注入错误[WHEA 管理 API](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)。 有关如何实现 WHEA 管理应用程序的详细信息，请参阅[WHEA 管理应用程序](whea-management-applications.md)。

 

 




