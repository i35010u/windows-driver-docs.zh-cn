---
title: 打印票证和功能-Unidrv/Pscript5
description: 打印票证和打印功能由 Unidrv/Pscript5 插件实现的提供程序接口
ms.assetid: 00dcbbde-e4e4-4fcc-b69f-9c91051e0e29
keywords:
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6da5595ecae2d97e87cc899815ce9f6e73f31e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372089"
---
# <a name="print-ticket-and-print-capabilities-provider-interface-implemented-by-unidrvpscript5-plug-ins"></a>打印票证和打印功能由 Unidrv/Pscript5 插件实现的提供程序接口


[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)(Unidrv) 和[Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md)(Pscript5) 核心打印机驱动程序在 Windows Vista 上的提供的插件来实现的打印票证的方法支持。 由于 Unidrv 和 Pscript5 都支持加载多个插件的单个驱动程序，每个插件是能够提供其自己的提供程序实现。 驱动程序供应商有责任确保每个 OEM 插件提供程序实现与其他人一起正常运行。 并非所有插件中的打印机驱动程序需要支持提供程序接口。 但是，核心驱动程序支持的版本的打印票证架构是核心驱动程序和所有可用的插件提供商支持的版本的子集。 由于调用插件的提供程序根据应用程序，必须以线程安全的方式实现插件的提供程序。

 




