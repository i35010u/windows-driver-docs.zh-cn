---
title: 正在处理库
description: 正在处理库
ms.assetid: 8ae9ae3b-885d-4eb5-b55b-415edcfc041a
keywords:
- 库 WDK Static Driver Verifier、 处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6b9e0aa920c28489b4638685868800fb29a5c35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525537"
---
# <a name="processing-a-library"></a>正在处理库


在运行之前验证，处理驱动程序需要的库。

 **若要处理库**

1.  启动的 Static Driver Verifier。 从**驱动程序**Visual Studio 菜单中的单击**启动 Static Driver Verifier...**.
2.  单击**库**选项卡，单击**添加库**添加库。
3.  导航到存储库的项目文件的目录。
4.  对于您的驱动程序使用每个库重复这些步骤。

Static Driver Verifier 保存的缓存，您将添加的库。 库所需驱动程序和缓存中将用于验证。 库会处理具有相同的驱动程序使用的配置和平台设置。

此外可以处理来自 Visual Studio 命令提示符窗口中使用的库**msbuild /t: / sdv p:"/ 输入 = / lib"** *libraryproject.vcxproj*选项。 有关命令选项的信息，请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。

如果您不能出于任何原因处理所需的库，您仍可以验证驱动程序使用它。 但是，结果是不太可靠的。

 

 





