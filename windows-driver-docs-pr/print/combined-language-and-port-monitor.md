---
title: 语言监视器与端口监视器的组合
description: 语言监视器与端口监视器的组合
keywords:
- 打印监视器 WDK，语言监视器
- 打印监视器 WDK，端口监视器
- 语言监视器 WDK 打印，端口监视器交互
- 端口监视 WDK 打印，语言监视器交互
- 组合语言和端口监视器 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92a9cba11c10b32f67acbbd7a87a5e476ad2f6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797671"
---
# <a name="combined-language-and-port-monitor"></a>语言监视器与端口监视器的组合





专用打印机硬件可由作为组合语言和端口监视器的单个自定义打印监视器支持。 如果此类监视器需要用户交互才能获取配置参数，则必须将其划分为 UI DLL 和服务器 DLL （遵循 [端口监视器](port-monitors.md)的模型）。 与语言相关的功能属于服务器 DLL。

组合监视器的 UI DLL 必须定义 [端口监视器客户端 dll 函数](port-monitor-client-dll-functions.md)。 其服务器 DLL 必须同时定义 [端口监视器服务器 dll 函数](port-monitor-server-dll-functions.md) 和 [语言监视器函数](language-monitor-functions.md)。

 

 




