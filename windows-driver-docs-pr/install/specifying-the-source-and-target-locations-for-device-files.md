---
title: 指定设备文件的源和目标位置
description: 指定设备文件的源和目标位置
ms.assetid: e44961e2-e9fb-43d3-aeb9-a625021e56e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59d25c19b848862a069ff4f8cd13d9649db4fd58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566947"
---
# <a name="specifying-the-source-and-target-locations-for-device-files"></a>指定设备文件的源和目标位置





在 Windows 进程复制、 重命名，并删除文件 INF 文件中的语句，它确定文件的源和目标位置。 若要确定这些位置，它将评估是否随操作系统一起或单独驱动程序，并探讨了各种 INF 文件的部分和项，包括**SourceDisksNames**， **SourceDisksFiles**，**包括**，**需要**，并且**DestinationDirs**。

本部分介绍 Windows 确定源和目标位置，和如何提供指导原则可帮助您正确指定这些位置，并介绍如何将 INF 文件从一个位置复制到另一个。 它包含以下主题：

[INF 文件的源媒体](source-media-for-inf-files.md)

[INF 文件的目标媒体](target-media-for-inf-files.md)

[复制 INF 文件](copying-inf-files.md)

 

 





