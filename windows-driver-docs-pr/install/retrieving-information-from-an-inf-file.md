---
title: 从 INF 文件中检索信息
description: 从 INF 文件中检索信息
ms.assetid: 4174357f-bca3-43b8-8ad6-331b9accd905
keywords:
- INF 文件 WDK 设备安装，检索信息
- 正在检索 INF 文件信息
- 状态信息 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bea78a426b680a1da7baa895aeec999b4475e1e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094973"
---
# <a name="retrieving-information-from-an-inf-file"></a>从 INF 文件中检索信息





获得 INF 文件的句柄后，可以通过多种方式从该句柄中检索信息。 [**SetupGetInfInformation**](/windows/desktop/api/setupapi/nf-setupapi-setupgetinfinformationa)、 [**SetupQueryInfFileInformation**](/windows/desktop/api/setupapi/nf-setupapi-setupqueryinffileinformationa)和[**SetupQueryInfVersionInformation**](/windows/desktop/api/setupapi/nf-setupapi-setupqueryinfversioninformationa)等函数检索有关指定 INF 文件的信息。

其他函数（如 [**SetupGetSourceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupgetsourceinfoa) 和 [**SetupGetTargetPath**](/windows/desktop/api/setupapi/nf-setupapi-setupgettargetpatha)）获取有关源文件和目标目录的信息。

[**SetupGetLineText**](/windows/desktop/api/setupapi/nf-setupapi-setupgetlinetexta)和[**SetupGetStringField**](/windows/desktop/api/setupapi/nf-setupapi-setupgetstringfielda)等函数使你能够直接访问存储在 INF 文件的行或字段中的信息。 这些函数由较高级别的 [setupapi.log](setupapi.md) 函数在内部使用，但如果必须直接访问行级或字段级别的信息，则可以使用这些函数。

 

