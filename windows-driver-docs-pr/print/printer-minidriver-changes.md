---
title: 打印机微型驱动程序更改
description: 打印机微型驱动程序更改
keywords:
- 内置自动配置支持 WDK 打印机，微型驱动程序更改
- GPD 文件 WDK 打印，内置自动配置支持
- GDL 文件 WDK 打印机
- PPD 文件 WDK 自动配置
- 插件 WDK 打印，内置自动配置支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e048e8cd90f5a1645d0053508024d6db200a7ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807239"
---
# <a name="printer-minidriver-changes"></a>打印机微型驱动程序更改


Printer 微型驱动程序包含打印机说明文件 (*GPD*、 *PPD* 或 GDL 文件) ，以及可选的用户界面 (UI) 插件、呈现插件和呈现筛选器。 对于内置包含，只允许一个 UI 插件，并且只允许一个 Unidrv 或 Pscript 呈现插件。 不允许将 IHV 端口监视器作为带有打印机微型驱动程序的内置机箱包括在内。

对于 GPD、PPD 或 GDL 文件，需要考虑两种情况：

-   添加到 GDL 文件： GDL 文件是取代 GPD 和 PPD 文件的打印机数据文件。

-   对其驱动程序已随 Windows 提供并且具有与之关联的 GPD 文件或 PPD 文件的打印机使用的现有 GPD 或 PPD 文件的修改。

以下主题描述了必须在驱动程序 UI 和打印机数据文件中进行的更改：

[UI 插件更改](ui-plug-in-changes.md)

[将 GDL 扩展添加到现有的 GPD 文件](adding-gdl-extensions-to-an-existing-gpd-file.md)

[将 GDL 扩展添加到现有的 PPD 文件](adding-gdl-extensions-to-an-existing-ppd-file.md)

[微型驱动程序 INI 文件中的 BidiFiles 项](bidifiles-entry-in-a-minidriver-s-ini-file.md)

[Pscript 和 Unidrv 微型驱动程序中的命名约定](naming-conventions-in-pscript-and-unidrv-minidrivers.md)

 

 




