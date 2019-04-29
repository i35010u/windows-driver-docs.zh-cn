---
title: 语言监视器与端口监视器的组合
description: 语言监视器与端口监视器的组合
ms.assetid: 5da362cf-92b8-4c78-80b2-57106b978600
keywords:
- 打印监视器 WDK，语言监视器
- 打印监视器 WDK，端口监视器
- 语言监视 WDK 打印，端口监视器交互
- 端口监视 WDK 打印，语言监视器交互
- 结合使用的语言和端口监视器 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c87cc2f2f7ffb9905ab91f84c2ccebfd42d4681
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357237"
---
# <a name="combined-language-and-port-monitor"></a>语言监视器与端口监视器的组合





可以通过单一的自定义打印监控器充当组合的语言和端口监视器支持专用的打印机硬件。 如果此类监视器需要用户交互来获取配置参数，它必须被划分到一个 UI DLL 和服务器 DLL，遵循的模型[端口监视器](port-monitors.md)。 与语言相关的功能位于服务器 DLL 中。

必须定义组合的监视器的 UI DLL[端口监视器客户端 DLL 函数](port-monitor-client-dll-functions.md)。 同时，必须定义其服务器 DLL[端口监视器服务器 DLL 函数](port-monitor-server-dll-functions.md)并[语言监视器函数](language-monitor-functions.md)。

 

 




