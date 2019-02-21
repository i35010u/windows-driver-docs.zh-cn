---
title: WDK 生成输出
description: 默认情况下，WDK 使用中间目录 $ （intdir） 宏来指定默认生成输出目录。
ms.assetid: CD083755-9C9C-458A-9115-E63336C413B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0756e08abee528387f0b870c5c511140960a1a98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540744"
---
# <a name="wdk-build-output"></a>WDK 生成输出


默认情况下使用的中间目录 WDK **$ （intdir)** 宏指定默认的生成输出目录。

WDK 定义所在的中间目录 **$ （platform)\\$ （configurationname)\\**。 **$ （configurationname)** 宏包括的目标版本的 Windows 和配置类型 （版本或调试），例如，x64\\Win8.1Release。

这样一来，可以生成不同的配置并行，而不会丢失上一个生成相同二进制文件的其他 Windows 目标。 这种方法是不同于在生成的 Windows 桌面应用程序，通常只包括平台 (x64，Win32) 和配置类型 （版本中，调试） 在名称中时可能使用的中间目录。

 

 





