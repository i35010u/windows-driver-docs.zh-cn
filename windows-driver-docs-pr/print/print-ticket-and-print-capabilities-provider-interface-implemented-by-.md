---
title: 打印票证和功能-Unidrv/Pscript5
description: Unidrv/Pscript5 插件实现的打印票证和打印功能提供程序接口
keywords:
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57e5236d75d17f8b616b55e3629ddca454a7e8e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807443"
---
# <a name="print-ticket-and-print-capabilities-provider-interface-implemented-by-unidrvpscript5-plug-ins"></a>Unidrv/Pscript5 插件实现的打印票证和打印功能提供程序接口


Windows Vista 上的 [Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md) (Unidrv) 和 [Microsoft PostScript 打印机驱动](microsoft-postscript-printer-driver.md) 程序 (Pscript5) 核心打印机驱动程序为插件提供实现打印票证支持的方法。 由于 Unidrv 和 Pscript5 都支持加载单个驱动程序的多个插件，因此每个插件都能提供自己的提供程序实现。 驱动程序供应商负责确保每个 OEM 插件提供程序实现都能正常地与其他实现一起工作。 并非打印机驱动程序中的所有插件都需要支持提供程序接口。 但是，核心驱动程序支持的打印票证架构版本是核心驱动程序和所有可用插件提供程序所支持的版本的子集。 因为对插件提供程序的调用由应用程序驱动，所以插件提供程序必须以线程安全的方式实现。

 




