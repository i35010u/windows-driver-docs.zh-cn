---
title: Windows Vista 中 GPD 的自动配置流
description: Windows Vista 中 GPD 的自动配置流
ms.assetid: 41468218-fa05-4431-a57d-3056449f2e2e
keywords:
- GPD 文件 WDK GDL 扩展，自动配置流
- 内置自动配置支持 WDK 打印机，步骤顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a8a92eff84165592aa9541c0374830a3f00c52b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842839"
---
# <a name="autoconfiguration-flow-for-gpd-in-windows-vista"></a>Windows Vista 中 GPD 的自动配置流


自动配置按照以下顺序进行：

1.  端口监视器向后台处理程序发送一个通知，其中包含以前不在缓存中或已更改的任何值。

2.  后台处理程序通过调用[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)来响应来自端口监视器的通知。

3.  打印机\_事件\_配置将传递到包含任何和所有新值的驱动程序。 将通知驱动程序属性的值已更改，同时还会更新注册表。

4.  如果通知太大，则会调用减少的架构事件。

5.  将分析 PPD 文件，包括 PPD 中的所有 GDL 文件扩展名和 GDL 内容。 GDL 文件扩展名或整个 PPD 文件中的所有 GDL 内容都必须在 **\*Ifdef**： GDL\_启用并且 **\*Endif**： GDL\_启用。

6.  插件将检索 **\*MSBidiValue**的值，这将基于 **\*QueryString**的当前字符串值。 例如，"\\DuplexUnit：已安装" 的 **\*QueryString**值将表示 **\*BidiValue**值 BOOL （TRUE）。

7.  插件将根据最新的配置更新驱动程序 UI。

 

 




