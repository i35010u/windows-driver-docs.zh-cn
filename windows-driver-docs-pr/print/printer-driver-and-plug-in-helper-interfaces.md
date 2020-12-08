---
title: 打印机驱动程序和插件帮助程序接口
description: 打印机驱动程序和插件帮助程序接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780af9b0843d4eaf1857e52890414eac8dcb691e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807319"
---
# <a name="printer-driver-and-plug-in-helper-interfaces"></a>打印机驱动程序和插件帮助程序接口


Windows Vista 及更高版本中提供的 [IPrintCoreHelper](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper) 接口提供了所有四核驱动程序模块（Unidrv 渲染、Unidrv 用户界面 (ui) 、Pscript5 渲染和 Pscript5 ui）中提供的基本功能。 为所有四个模块提供单个接口，原因如下：

-   接口反映基础结构。

-   接口提供编写通用代码模块的功能，以使插件执行某些行为，如约束解析。

你可以使用 **IPrintCoreHelper** 接口为基于 Unidrv 和 Pscript5 的驱动程序编写单一 UI 替换插件。

由于 Pscript5 和 Unidrv 驱动程序基础结构之间的差异，有两个附加接口 [IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni) 和 [IPrintCoreHelperPS](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)，它们继承自 **IPrintCoreHelper** 接口，并提供基于各个驱动程序的扩展服务。 这些接口仅在各自的模块中可用。 Pscript5 helper interface， **IPrintCoreHelperPS** 提供对某些 PostScript 打印机说明 (PPD) 数据的访问，而 Unidrv helper Interface， **IPrintCoreHelperUni** 提供了通过 GPD 分析器（Windows Vista 的新增功能）访问通用打印机配置 (GDL) 文件的功能。

本部分提供下列主题：

[插件的 Unidrv 和 Pscript5 帮助程序接口](unidrv-and-pscript5-helper-interfaces-for-plug-ins.md)

[发布接口](publishing-the-interfaces.md)

[IPrintCoreHelper 接口详细信息](details-of-the-iprintcorehelper-interface.md)

 

