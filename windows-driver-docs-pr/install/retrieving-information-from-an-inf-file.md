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
ms.openlocfilehash: 450bc5bc7cc5a7c02918c42a745def6afde25d95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382286"
---
# <a name="retrieving-information-from-an-inf-file"></a>从 INF 文件中检索信息





后一个句柄到 INF 文件，可以从它在不同的方式来检索信息。 之类的函数[ **SetupGetInfInformation**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetinfinformationa)， [ **SetupQueryInfFileInformation**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryinffileinformationa)，并[ **SetupQueryInfVersionInformation** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryinfversioninformationa)检索有关指定的 INF 文件的信息。

其他函数，如[ **SetupGetSourceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetsourceinfoa)并[ **SetupGetTargetPath**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgettargetpatha)，获取有关在源代码文件的信息和目标目录。

之类的函数[ **SetupGetLineText** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetlinetexta)并[ **SetupGetStringField** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetstringfielda)使你能够直接访问存储中的信息行或字段的 INF 文件。 这些函数内部使用的更高级别的[SetupAPI](setupapi.md)函数但是如果您需要直接访问级别的行或字段信息可用。

 

 





