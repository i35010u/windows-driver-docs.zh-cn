---
title: WDK 生成输出
description: 默认情况下，WDK 使用中间目录 $ (IntDir) 宏来指定默认的生成输出目录。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3b024771913636100eac935860271fc68b5c454
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830097"
---
# <a name="wdk-build-output"></a>WDK 生成输出


默认情况下，WDK 使用中间目录 **$ (IntDir)** 宏来指定默认的生成输出目录。

WDK 将中间目录定义为 **$ (平台) \\ $ (ConfigurationName) \\**。 **$ (ConfigurationName)** 宏包括目标版本的 Windows 和配置类型 (发布或调试) ，例如 x64 \\ win 8.1 版本。

通过这种方式，可以并行生成不同的配置，而不会丢失相同二进制文件的其他 Windows 目标的以前版本。 此方法不同于生成 Windows 桌面应用程序时可能使用的中间目录，该应用程序通常仅包括平台 (x64、Win32) 以及名称中 (Release，调试) 的配置类型。

 

 





