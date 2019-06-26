---
title: Windows Vista 中 GPD 的自动配置流
description: Windows Vista 中 GPD 的自动配置流
ms.assetid: 41468218-fa05-4431-a57d-3056449f2e2e
keywords:
- GPD 文件 WDK GDL 扩展，自动配置流
- 框中自动配置支持 WDK 打印机的步骤顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc54fd9a9b856405abd1775f54c50f00f8aa355e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370473"
---
# <a name="autoconfiguration-flow-for-gpd-in-windows-vista"></a>Windows Vista 中 GPD 的自动配置流


自动配置为按以下顺序：

1.  端口监视器将包含以前已不在缓存或更改任何值的通知发送到后台处理程序。

2.  后台处理程序响应的通知从端口监视器通过调用[ **DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent)。

3.  打印机\_事件\_配置传递给驱动程序包含所有新值。 属性的值已更改，并且也会更新注册表，则会通知驱动程序。

4.  如果通知是太大，会调用减少架构事件。

5.  PPD 文件进行分析，包括所有 GDL 文件扩展名和中 PPD.GDL 内容 所有 GDL 内容中任一 GDL 文件扩展名或在整个 PPD 文件必须用都括 **\*Ifdef**:GDL\_已启用并 **\*Endif**:GDL\_启用。

6.  插件将检索的值 **\*MSBidiValue**，将基于当前的字符串值 **\*QueryString**。 例如，  **\*QueryString**的值"\\Printer.Configuration.DuplexUnit:Installed"将表示 **\*BidiValue** BOOL(TRUE) 的值。

7.  插件将根据最新的配置中更新驱动程序用户界面。

 

 




