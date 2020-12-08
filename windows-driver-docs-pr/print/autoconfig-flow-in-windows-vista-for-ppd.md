---
title: Windows Vista 中的 PPD 自动配置流
description: Windows Vista 中的 PPD 自动配置流
keywords:
- PPD 文件 WDK 自动配置，步骤顺序
- 内置自动配置支持 WDK 打印机，步骤顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c86495c7b6ebcd120f52612ad32d6ea69c9acd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836145"
---
# <a name="autoconfig-flow-in-windows-vista-for-ppd"></a>Windows Vista 中的 PPD 自动配置流


自动配置遵循以下顺序：

1.  端口监视器向后台处理程序发送一个通知，其中包含以前不在缓存中或已更改的任何值。

2.  后台处理程序通过调用 DrvPrinterEvent 来响应来自端口监视器的通知。

3.  将打印机 \_ 事件 \_ 配置传递到包含任何和所有新值的驱动程序。 将通知驱动程序属性的值已更改。 还会更新注册表。

4.  如果通知太大，则会调用减少的架构事件。

5.  对 PPD 文件进行分析，包括 PPD 中的所有 GDL 文件扩展名和 GDL 内容。 GDL 文件扩展名或整个 PPD 文件中的所有 GDL 内容都必须与和环绕 `*Ifdef: GDL_Enabled` `*Endif: GDL_Enabled` 。

6.  IHV 插件将检索 **\* MSBidiValue** 的值，这将基于 **\* QueryString** 的当前字符串值。 例如，Printer.Configu 的 **\* 查询字符串** 值 \\ 。DuplexUnit：已安装将表示 BOOL (TRUE) 的 **\* BidiValue** 值。

7.  IHV 插件将根据最新的配置更新驱动程序 UI。

 

 




