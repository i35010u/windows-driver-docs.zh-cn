---
title: XPSDrv 驱动程序建议
description: XPSDrv 驱动程序建议
ms.assetid: 6700afd2-8526-4464-92b8-a9c1a37f8402
keywords:
- 版本 3 的 XPS 驱动程序 WDK XPSDrv，建议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cae981451f5fc77b5e42f2e50ae7c8f58a1f0b70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523031"
---
# <a name="xpsdrv-driver-recommendations"></a>XPSDrv 驱动程序建议


除了[XPSDrv 驱动程序要求](xpsdrv-driver-requirements.md)，应考虑以下最佳实践：

-   **使用模块化 GPD 或 PPD 文件。** 对于基于 Unidrv 或 PScript5 基于配置的模块，打印驱动程序应提供每个筛选器的单独 GPD 或 PPD 文件。 然后，单个"父级"打印驱动程序 GPD 或 PPD 文件应引用的所有每个筛选器 GPD 或 PPD 文件。 筛选器按组织中模块化方式的 GPD 和 PPD 文件可帮助维护的模块化和重复使用的筛选器管道中的筛选器。

-   **将映射到公共打印架构关键字。** 只要有可能，应映射所有打印驱动程序设置和打印驱动程序能力中公共打印架构及其等效关键字。 映射到公共打印架构关键字的打印驱动程序设置，便于应用程序采用新功能。 此映射还提供了更好地同步的打印驱动程序和应用程序和系统之间的打印机设置。

 

 




