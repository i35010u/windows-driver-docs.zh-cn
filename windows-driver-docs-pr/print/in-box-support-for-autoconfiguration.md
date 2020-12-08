---
title: 现成的自动配置支持
description: 现成的自动配置支持
keywords:
- 自动配置 WDK 打印机，内置支持
- 打印机自动配置 WDK 打印机，内置支持
- 内置自动配置支持 WDK 打印机
- 内置自动配置支持 WDK 打印机，关于内置自动配置支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7bdba3e0f8a4686d728af90f3e5fda44ec022fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835713"
---
# <a name="in-box-support-for-autoconfiguration"></a>现成的自动配置支持


在 Windows Vista 中，使用标准 TCP/IP 端口监视器或适用于设备 (WSD) 端口监视器的基于 Unidrv 和 Pscript5 的驱动程序为自动配置提供支持。 请注意，Windows Vista 中的自动配置支持仅提供有关可安装功能的查询，例如与双工单元或字体盒相关的查询。 对于给定的功能，对查询的响应只能涉及功能的一个选项。 有关双工单元是否安装的查询会得出以下两个响应之一：已安装双面打印单元或它不是。 查询安装了哪一种字体盒会生成一个响应，该响应指明字体盒 *a* 已安装，或是安装了字体盒 *B* 。

自动配置的当前 (版本 1) 实现不允许多个响应。 查询仅限于一个功能选项。 例如，这意味着对查询的响应不能提供有关输入托盘中的介质大小和介质颜色的信息。

以下主题介绍如何利用 Windows Vista 中的自动配置的内置支持：

[打印机微型驱动程序更改](printer-minidriver-changes.md)

[自定义打印机端口监视器](customizing-the-printer-port-monitors.md)

 

 




