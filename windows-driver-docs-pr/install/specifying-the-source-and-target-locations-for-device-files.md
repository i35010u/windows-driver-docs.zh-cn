---
title: 指定设备文件的源和目标位置
description: 指定设备文件的源和目标位置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a78acbc89254aa73fe2f662d6544761792cca9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813077"
---
# <a name="specifying-the-source-and-target-locations-for-device-files"></a>指定设备文件的源和目标位置





当 Windows 处理 INF 文件中的复制、重命名和删除文件语句时，它将确定文件的源位置和目标位置。 若要确定这些位置，请评估该驱动程序是随操作系统一起提供的还是单独的，并检查各种 INF 文件部分和条目，包括 **SourceDisksNames**、 **SourceDisksFiles**、 **Include**、 **需要** 和 **DestinationDirs**。

本部分介绍 Windows 如何确定源位置和目标位置，并提供帮助您正确指定这些位置的指南，并说明如何将 INF 文件从一个位置复制到另一个位置。 本节包含以下主题：

[INF 文件的源媒体](source-media-for-inf-files.md)

[INF 文件的目标媒体](target-media-for-inf-files.md)

[复制 INF 文件](copying-inf-files.md)

 

 





