---
title: 打印机驱动程序和插件帮助程序接口
description: 打印机驱动程序和插件帮助程序接口
ms.assetid: 21e5ae44-01e8-4f80-8d67-18e4d9c190c5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd4dbdfab77398351c4b3b328abbc068768ced31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380646"
---
# <a name="printer-driver-and-plug-in-helper-interfaces"></a>打印机驱动程序和插件帮助程序接口


[IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper)接口，这是在 Windows Vista 及更高版本，提供的基本功能，可在所有四个核心驱动程序模块-Unidrv 呈现，Unidrv 用户界面 (UI) Pscript5 呈现和 Pscript5 UI。 所有四个模块中提供，一个接口，因为：

-   界面将反映基础体系结构。

-   接口提供了用于编写插件执行某些行为，例如，约束分辨率的常见代码模块的功能。

可以使用**IPrintCoreHelper**接口编写单个 UI 替换插件适用于基于 Unidrv 和基于 Pscript5 的驱动程序。

由于 Pscript5 和 Unidrv 驱动程序基础结构之间的差异，有两个其他接口[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)并[IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)，继承自**IPrintCoreHelper**接口，并提供单个驱动程序的扩展的服务。 这些接口是仅在其各自的模块中可用。 Pscript5 帮助程序接口**IPrintCoreHelperPS**，提供对某些 PostScript 打印机说明 (PPD) 数据，而 Unidrv 帮助程序接口，访问**IPrintCoreHelperUni**，提供了若要访问通用打印机配置 (GPD) 文件通过 GDL 分析器，这是适用于 Windows Vista 的新增功能。

本部分提供了以下主题：

[Unidrv 和 Pscript5 帮助程序接口的插件](unidrv-and-pscript5-helper-interfaces-for-plug-ins.md)

[发布这些接口](publishing-the-interfaces.md)

[IPrintCoreHelper 接口的详细信息](details-of-the-iprintcorehelper-interface.md)

 

 




