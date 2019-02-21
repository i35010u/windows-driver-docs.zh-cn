---
title: 自动配置 PPD 的 Windows Vista 中的流
description: 自动配置 PPD 的 Windows Vista 中的流
ms.assetid: 60675cd3-fe98-4772-aa1b-a73529480d8a
keywords:
- PPD 文件 WDK 自动配置，一系列步骤
- 框中自动配置支持 WDK 打印机的步骤顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e1cf59884967bd56de4f0af8c3040a26a55eeda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554908"
---
# <a name="autoconfig-flow-in-windows-vista-for-ppd"></a>自动配置 PPD 的 Windows Vista 中的流


自动配置为按以下顺序：

1.  端口监视器将包含以前已不在缓存或更改任何值的通知发送到后台处理程序。

2.  后台处理程序响应的通知从端口监视器通过调用 DrvPrinterEvent。

3.  打印机\_事件\_配置传递给驱动程序包含所有新值。 属性值已更改通知驱动程序。 此外更新注册表。

4.  如果通知是太大，称为减少架构事件。

5.  PPD 进行分析，包括所有 GDL 文件扩展名和中 PPD.GDL 内容 所有 GDL 内容中任一 GDL 文件扩展名或在整个 PPD 文件必须用都括`*Ifdef: GDL_Enabled`和`*Endif: GDL_Enabled`。

6.  插件 IHV 将检索的值 **\*MSBidiValue**将基于当前的字符串值 **\*QueryString**。 例如，  **\*QueryString**的值\\Printer.Configuration.DuplexUnit:Installed 将表示 **\*BidiValue** BOOL(TRUE) 的值。

7.  IHV 插件将根据最新配置更新驱动程序用户界面。

 

 




