---
title: 处理库
description: 处理库
keywords:
- 库 WDK 静态驱动程序验证程序，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d668b243d63f0924cec0889d2faacf636934f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783301"
---
# <a name="processing-a-library"></a>处理库


在运行验证之前，请处理驱动程序所需的库。

 **处理库**

1.  启动 "静态驱动程序验证程序"。 在 Visual Studio 中的 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。
2.  单击 " **库** " 选项卡，然后单击 " **添加库** " 以添加库。
3.  导航到存储库的项目文件的目录。
4.  为驱动程序使用的每个库重复这些步骤。

静态驱动程序验证程序保留你添加的库的缓存。 只有驱动程序所需的库和缓存中提供的库才会用于验证。 使用驱动程序使用的相同配置和平台设置来处理库。

还可以使用 **msbuild t：/sdv p： "/Inputs =/lib"** *libraryproject .Vcxproj* 选项处理 Visual Studio 命令提示符窗口中的库。 有关命令选项的信息，请参阅 [静态驱动程序验证程序命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)。

如果出于任何原因无法处理所需的库，仍可以验证使用它的驱动程序。 但是，结果不太可靠。

 

 





