---
title: 打开和关闭 INF 文件
description: 打开和关闭 INF 文件
ms.assetid: da270688-4b8b-43b3-afdb-8f31d15ef50c
keywords:
- INF 文件 WDK 设备安装，打开
- INF 文件 WDK 设备安装，关闭
- 打开 INF 文件
- 关闭 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0d9c51de3d8ce071cd64e2b63d50f16581227fc
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716166"
---
# <a name="opening-and-closing-an-inf-file"></a>打开和关闭 INF 文件





在 *设备安装应用程序* 可以访问 INF 文件中的信息之前，必须通过调用 [**SetupOpenInfFile**](/windows/win32/api/setupapi/nf-setupapi-setupopeninffilea)打开该文件。 此函数返回 INF 文件的句柄。

如果你不知道必须打开的 INF 文件的名称，请使用 [**SetupGetInfFileList**](/windows/win32/api/setupapi/nf-setupapi-setupgetinffilelista) 获取目录中所有 inf 文件的列表。

应用程序打开 INF 文件后，可以将其他 INF 文件附加到使用 [**SetupOpenAppendInfFile**](/windows/win32/api/setupapi/nf-setupapi-setupopenappendinffilea)的已打开文件。 当后续 [setupapi.log](setupapi.md) 函数引用打开的 INF 文件时，它们还将能够访问任何附加文件中存储的任何信息。

如果在调用[**SetupOpenAppendInfFile**](/windows/win32/api/setupapi/nf-setupapi-setupopenappendinffilea)时未指定 inf 文件，则此函数会将**LayoutFile**条目指定的文件追加到在调用[**SetupOpenInfFile**](/windows/win32/api/setupapi/nf-setupapi-setupopeninffilea)期间打开的 inf 文件的[**inf 版本部分**](inf-version-section.md)中。

当不再需要 INF 文件中的信息时，应用程序应调用 [**SetupCloseInfFile**](/windows/win32/api/setupapi/nf-setupapi-setupcloseinffile) 来释放在调用 [**SetupOpenInfFile**](/windows/win32/api/setupapi/nf-setupapi-setupopeninffilea)期间分配的资源。

 

