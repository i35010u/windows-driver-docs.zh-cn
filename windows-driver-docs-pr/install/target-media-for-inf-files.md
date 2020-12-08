---
title: INF 文件的目标媒体
description: INF 文件的目标媒体
keywords:
- INF 文件 WDK 设备安装，目标介质
- 目标 media WDK INF 文件
- 位置 WDK INF 文件
- media WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bce88e0fb466ebf7b94de1e50f3b49592159867a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826797"
---
# <a name="target-media-for-inf-files"></a>INF 文件的目标媒体





INF 文件指定具有 [**DestinationDirs**](inf-destinationdirs-section.md) 节的设备文件的目标位置。 应始终在与复制、重命名或删除语句部分相同的 INF 文件中指定此部分。

**DestinationDirs** 部分应包含 **DefaultDestDir** 条目。

如果 INF 有复制、重命名或删除部分，但没有 **DestinationDirs** 部分，并且 inf 包含其他 inf 文件，则 Windows 将在包含的 inf 文件中搜索目标位置信息。 但是，Windows 搜索包含的文件的顺序是不可预测的。 因此，Windows 会面临一些风险，例如，将文件复制到 INF 编写器不应使用的位置。 若要避免此类混淆，请始终在 INF 中指定包含复制、重命名或删除部分的 **DestinationDirs** 部分。 **DestinationDirs** 节应该至少包含一个 **DefaultDestDir** 条目，并且可以列出 INF 中复制、重命名或删除文件的部分。

 

 





