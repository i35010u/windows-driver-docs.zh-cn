---
title: WDK 和 MSBuild 概述
description: Visual Studio 可以管理多个项目。 本部分介绍了 WDK 生成环境。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aff5df9eb54adaba9972e2302533b3958f2eae5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823317"
---
# <a name="wdk-and-msbuild-overview"></a>WDK 和 MSBuild 概述


Visual Studio 可以管理多个项目。 本部分介绍了 WDK 生成环境。

Visual Studio 解决方案可以包含一个或多个项目：驱动程序项目和非驱动程序项目。 每个项目都与一个平台工具集相关联。 平台工具集可扩展和修改给定目标体系结构的生成过程，以便生成特定类型的二进制文件。 二进制文件可以是驱动程序、库或可执行程序。

下图显示了使用 MSBuild 平台的典型生成过程。 在关系图中， (MSBuild 项目 1) 的驱动程序项目使用驱动程序平台工具集来生成驱动程序。 驱动程序项目可以引用 Windows 内核模式和用户模式的标头和库。 Windows DLL 项目 (MSBuild 项目 2) 生成一个 DLL，并使用 Windows SDK 平台工具集来生成应用程序或用户模式库。 每个平台工具集都有其自己的目标集。 这些目标调用任务。 这些任务将执行生成工具。

对于 C/c + + 本机代码 (用户模式和内核模式) 和托管代码，WDK 会安装 .NET Full Framework、Windows 标头、库 (用户模式或内核模式) 和工具、.NET 工具和 VC 编译器、CRT 标头和库。 为了能够使用 MSBuild 生成 C/c + + 项目，必须安装编译器所需的所有组件。

![图显示了 visual studio 驱动程序解决方案的 wdk 和 msbuild 平台。](images/build-platform-msbuild.png)

 

 





