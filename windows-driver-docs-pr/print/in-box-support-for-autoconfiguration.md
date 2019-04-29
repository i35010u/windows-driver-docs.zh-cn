---
title: 现成的自动配置支持
description: 现成的自动配置支持
ms.assetid: cd2faef4-96ba-4d11-99f6-90e41ae2e283
keywords:
- 自动配置 WDK 打印机，现成的支持
- 打印机自动配置 WDK 打印机的内置支持
- 框中自动配置支持 WDK 打印机
- 框中自动配置支持 WDK 打印机，在框中自动配置支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3731dbb9b5a6ff6505bcaf7b5050ca2f65705cb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390561"
---
# <a name="in-box-support-for-autoconfiguration"></a>现成的自动配置支持


在 Windows Vista 中，使用标准 TCP/IP 端口监视器或 Web Services for Devices (WSD) 端口监视器 Unidrv 基于和基于 Pscript5 的驱动程序自动配置为提供支持。 请注意，仅提供有关可安装的功能，例如那些关心双面打印单元或字体盒查询 Windows Vista 中的自动配置支持。 对于给定的功能，对查询的响应可以与该功能只提供一个选项。 有关是否安装了双面打印单元的查询会引出两个响应之一： 已安装的双面打印单元或者字段不是。 查询有关哪种字体安装插件将生成一个响应指示任一此字体盒式磁带*A*已安装或此字体盒式磁带*B*已安装。

自动配置的当前 （版本 1） 实现不允许对多个响应。 查询是限于一项功能的单个选项。 例如，这意味着在送纸器中的大小和介质颜色对查询的响应不能提供有关这两个媒体的信息。

以下主题介绍如何利用 Windows Vista 中的自动配置的内置支持：

[打印机微型驱动程序更改](printer-minidriver-changes.md)

[自定义的打印机端口监视器](customizing-the-printer-port-monitors.md)

 

 




