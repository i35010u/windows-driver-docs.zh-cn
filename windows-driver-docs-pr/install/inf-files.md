---
title: INF 文件
description: INF 文件
ms.assetid: 8557a072-1b08-41f9-8c35-976a96ff639c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d287fb092116f1d8768afeaecb42a7184688126c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391986"
---
# <a name="inf-files"></a>INF 文件


Windows 使用安装程序信息 (INF) 文件来安装设备的以下组件：

-   一个或多个驱动程序支持的设备。

-   特定于设备的配置或设置要将设备联机。

可以使用*INX*文件以自动创建一个 INF 文件。 INX 文件是包含表示版本信息的字符串变量的 INF 文件。 生成实用工具和[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具将替换文本字符串，表示特定硬件体系结构或 framework 版本为 INX 文件中的字符串变量。 有关 INX 文件的详细信息，请参阅[使用 INX 文件转换为创建 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff545473)。

本部分包括以下主题：

-   [INF 文件概述](overview-of-inf-files.md)
-   [从设备安装应用程序访问 INF 文件](accessing-inf-files-from-a-setup-application.md)
-   [提供 Shell 和自动播放的供应商图标](providing-vendor-icons-for-the-shell-and-autoplay.md)

 

 





