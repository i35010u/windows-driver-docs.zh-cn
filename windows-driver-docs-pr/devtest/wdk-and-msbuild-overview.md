---
title: WDK 和 MSBuild 概述
description: Visual Studio 可以管理多个项目。 本部分介绍 WDK 构建环境。
ms.assetid: BABF3C72-05E9-4424-AAF9-68DFD48CEC32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd24d1284ab15fa62441deaa79b22aa9ce9ed7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371567"
---
# <a name="wdk-and-msbuild-overview"></a>WDK 和 MSBuild 概述


Visual Studio 可以管理多个项目。 本部分介绍 WDK 构建环境。

Visual Studio 解决方案可包含单个项目或多个项目： 驱动程序项目和非驱动程序项目。 每个项目都与平台工具集关联。 平台工具集扩展，并修改给定的目标体系结构的生成过程以生成特定类型的二进制文件。 驱动程序、 库或可执行程序，可以是二进制文件。

下图显示了使用 MSBuild 平台的典型生成过程。 在关系图中，驱动程序项目 (MSBuild 项目 1) 使用驱动程序的平台工具集生成驱动程序。 驱动程序项目可以引用 Windows 内核模式和用户模式下的标头和库。 Windows DLL 项目 (MSBuild 项目 2) 生成一个 DLL，并使用 Windows SDK 平台工具集来生成应用程序或用户模式库。 每个平台工具集都有其自己的目标集。 这些目标调用任务。 生成工具将执行这些任务。

对于 C /C++ （用户模式和内核模式） 的本机代码和托管的代码，WDK 安装.NET Full Framework、 Windows 标头、 库 （用户模式或内核模式） 和工具、.NET 工具和 VC 编译器、 CRT 标头和库。 以及这些数据，以便能够生成 C /C++必须安装使用 MSBuild 时，由编译器所需的所有组件项目。

![图显示了 visual studio 驱动程序解决方案的 wdk 和 msbuild 平台。](images/build-platform-msbuild.png)

 

 





