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
ms.openlocfilehash: 4c5e4370719e045898cbe778a403455c8262c7a9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715089"
---
# <a name="retrieving-information-from-an-inf-file"></a>从 INF 文件中检索信息





获得 INF 文件的句柄后，可以通过多种方式从该句柄中检索信息。 [**SetupGetInfInformation**](/windows/win32/api/setupapi/nf-setupapi-setupgetinfinformationa)、 [**SetupQueryInfFileInformation**](/windows/win32/api/setupapi/nf-setupapi-setupqueryinffileinformationa)和[**SetupQueryInfVersionInformation**](/windows/win32/api/setupapi/nf-setupapi-setupqueryinfversioninformationa)等函数检索有关指定 INF 文件的信息。

其他函数（如 [**SetupGetSourceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupgetsourceinfoa) 和 [**SetupGetTargetPath**](/windows/win32/api/setupapi/nf-setupapi-setupgettargetpatha)）获取有关源文件和目标目录的信息。

[**SetupGetLineText**](/windows/win32/api/setupapi/nf-setupapi-setupgetlinetexta)和[**SetupGetStringField**](/windows/win32/api/setupapi/nf-setupapi-setupgetstringfielda)等函数使你能够直接访问存储在 INF 文件的行或字段中的信息。 这些函数由较高级别的 [setupapi.log](setupapi.md) 函数在内部使用，但如果必须直接访问行级或字段级别的信息，则可以使用这些函数。

 

