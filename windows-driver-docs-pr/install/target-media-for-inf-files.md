---
title: INF 文件的目标媒体
description: INF 文件的目标媒体
ms.assetid: f1aaea38-e500-40a9-89c1-9c4447054fb1
keywords:
- INF 文件 WDK 设备安装，目标媒体
- 目标媒体 WDK INF 文件
- 位置 WDK INF 文件
- 媒体 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 019e858cc076734496c1d90a69be0ea69eb15d7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339608"
---
# <a name="target-media-for-inf-files"></a>INF 文件的目标媒体





INF 文件指定了的设备文件的目标位置[ **DestinationDirs** ](inf-destinationdirs-section.md)部分。 本部分应始终指定相同的 INF 文件中，为与复制的部分重命名或删除语句。

一个**DestinationDirs**部分中应包括**DefaultDestDir**条目。

如果 INF 具有副本，重命名或删除部分，但不是删除**DestinationDirs**部分和 INF 包括其他 INF 文件，Windows 将搜索包含的 INF 文件中的目标位置信息。 但是，Windows 搜索包含的文件的顺序不是可预测的。 因此，没有风险，Windows 将例如，将文件复制到不应由 INF 编写器的位置。 若要避免此类冲突，请始终指定**DestinationDirs**部分中包含副本 INF，重命名或删除的分区。 **DestinationDirs**部分中应包括至少**DefaultDestDir**条目可以列出 INF 的复制、 重命名或删除文件的部分。

 

 





