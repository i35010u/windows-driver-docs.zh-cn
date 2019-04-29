---
title: 打印机微型驱动程序更改
description: 打印机微型驱动程序更改
ms.assetid: 8f427642-a758-48bf-96e1-95a27adbaf23
keywords:
- 在框中自动配置支持 WDK 打印机，微型驱动程序更改
- GPD 文件 WDK 打印、 框中自动配置支持
- GDL 文件 WDK 打印机
- PPD 文件 WDK 自动配置
- 插件 WDK 打印、 框中自动配置支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29dcdfe0ac9a9b7c8e613af3c4892d78a28e5444
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384602"
---
# <a name="printer-minidriver-changes"></a>打印机微型驱动程序更改


打印机微型驱动程序包含打印机说明文件 (*GPD*， *PPD*，或 GDL 文件)，以及可选的用户界面 (UI) 插件、 呈现插件和呈现筛选器。 框中包含存在只有一个 UI 插件，并且只有一个 Unidrv 或 Pscript 呈现插件允许使用。 不允许 IHV 端口监视器，以将其包含现成使用打印机微型驱动程序。

GPD、 PPD 或 GDL 文件中，有两种情况需要考虑：

-   GDL 文件的新增功能：GDL 文件是取代 GPD 的打印机的数据文件和 PPD 文件。

-   修改现有 GPD 或 PPD 文件用于的打印机的驱动程序已随 Windows 且具有 GPD 文件或与之关联的 PPD 文件。

以下主题介绍了必须在驱动程序 UI 和打印机的数据文件中所做的更改：

[更改 UI 插件](ui-plug-in-changes.md)

[将 GDL 扩展添加到现有的 GPD 文件](adding-gdl-extensions-to-an-existing-gpd-file.md)

[将 GDL 扩展添加到现有的 PPD 文件](adding-gdl-extensions-to-an-existing-ppd-file.md)

[BidiFiles 微型驱动程序的 INI 文件中的条目](bidifiles-entry-in-a-minidriver-s-ini-file.md)

[Pscript 和 Unidrv 微型驱动程序中的命名约定](naming-conventions-in-pscript-and-unidrv-minidrivers.md)

 

 




