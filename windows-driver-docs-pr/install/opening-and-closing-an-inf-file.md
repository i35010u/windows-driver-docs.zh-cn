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
ms.openlocfilehash: b13f64fa14fc1d9139ab16a39af28c9486ac4ccc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366661"
---
# <a name="opening-and-closing-an-inf-file"></a>打开和关闭 INF 文件





之前*设备安装应用程序*可以访问 INF 文件中的信息，它必须通过调用来打开文件[ **SetupOpenInfFile**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupopeninffilea)。 此函数返回的句柄的 INF 文件。

如果不知道需要打开，可使用 INF 文件的名称[ **SetupGetInfFileList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetinffilelista)来获取目录中的所有 INF 文件列表。

一旦应用程序打开一个 INF 文件，它可以将其他 INF 文件追加到所使用的打开文件[ **SetupOpenAppendInfFile**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupopenappendinffilea)。 当后续[SetupAPI](setupapi.md)函数引用打开的 INF 文件，还将能够访问存储在任何附加的文件中的任何信息。

如果调用时指定没有 INF 文件[ **SetupOpenAppendInfFile**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupopenappendinffilea)，此函数将由指定的文件追加**LayoutFile**中的条目[ **INF 版本部分**](inf-version-section.md) INF 文件的打开到在调用期间[ **SetupOpenInfFile**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupopeninffilea)。

当不再需要 INF 文件中的信息时，应用程序应调用[ **SetupCloseInfFile** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcloseinffile)释放资源分配到在调用期间[ **SetupOpenInfFile**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupopeninffilea)。

 

 





