---
title: 从 INF 文件中检索信息
description: 从 INF 文件中检索信息
ms.assetid: 4174357f-bca3-43b8-8ad6-331b9accd905
keywords:
- INF 文件 WDK 设备安装，检索信息
- 检索 INF 文件信息
- 状态信息 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e304467888391b5856db1f6717a439e9de470eb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363320"
---
# <a name="retrieving-information-from-an-inf-file"></a>从 INF 文件中检索信息





后一个句柄到 INF 文件，可以从它在不同的方式来检索信息。 之类的函数[ **SetupGetInfInformation**](https://msdn.microsoft.com/library/windows/desktop/aa377383)， [ **SetupQueryInfFileInformation**](https://msdn.microsoft.com/library/windows/desktop/aa377416)，并[ **SetupQueryInfVersionInformation** ](https://msdn.microsoft.com/library/windows/desktop/aa377418)检索有关指定的 INF 文件的信息。

其他函数，如[ **SetupGetSourceInfo** ](https://msdn.microsoft.com/library/windows/desktop/aa377392)并[ **SetupGetTargetPath**](https://msdn.microsoft.com/library/windows/desktop/aa377394)，获取有关在源代码文件的信息和目标目录。

之类的函数[ **SetupGetLineText** ](https://msdn.microsoft.com/library/windows/desktop/aa377388)并[ **SetupGetStringField** ](https://msdn.microsoft.com/library/windows/desktop/aa377393)使你能够直接访问存储中的信息行或字段的 INF 文件。 这些函数内部使用的更高级别的[SetupAPI](setupapi.md)函数但是如果您需要直接访问级别的行或字段信息可用。

 

 





