---
title: XPSDrv 驱动程序建议
description: XPSDrv 驱动程序建议
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv，建议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b62db84789ab1685abbe78adaa37a2ee8e418500
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785711"
---
# <a name="xpsdrv-driver-recommendations"></a>XPSDrv 驱动程序建议


除了 [XPSDrv 驱动程序要求](xpsdrv-driver-requirements.md)之外，还应考虑以下最佳做法：

-   **使用模块化 GPD 或 PPD 文件。** 对于基于 Unidrv 或 PScript5 的配置模块，打印驱动程序应为每个筛选器提供单独的 GPD 或 PPD 文件。 然后，单个 "parent" 打印驱动程序 GPD 或 PPD 文件应引用每个筛选器的 GPD 或 PPD 文件。 通过筛选器以模块化方式组织 GPD 和 PPD 文件，有助于在筛选器管道中维护筛选器的模块化和重复使用。

-   **映射到公共打印架构关键字。** 应尽可能将所有打印驱动程序设置和打印驱动程序的 capabilitiesto 映射到公共打印架构中的等效关键字。 将打印驱动程序设置映射到公共打印架构关键字，使应用程序能够更轻松地采用新功能。 此映射还可以更好地同步打印驱动程序和应用程序与系统之间的打印机设置。

 

 




