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
ms.openlocfilehash: 7234e51fdcf5def3aa4557fd0ced3861be2c8232
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566030"
---
# <a name="opening-and-closing-an-inf-file"></a>打开和关闭 INF 文件





之前*设备安装应用程序*可以访问 INF 文件中的信息，它必须通过调用来打开文件[ **SetupOpenInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377409)。 此函数返回的句柄的 INF 文件。

如果不知道需要打开，可使用 INF 文件的名称[ **SetupGetInfFileList** ](https://msdn.microsoft.com/library/windows/desktop/aa377381)来获取目录中的所有 INF 文件列表。

一旦应用程序打开一个 INF 文件，它可以将其他 INF 文件追加到所使用的打开文件[ **SetupOpenAppendInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377407)。 当后续[SetupAPI](setupapi.md)函数引用打开的 INF 文件，还将能够访问存储在任何附加的文件中的任何信息。

如果调用时指定没有 INF 文件[ **SetupOpenAppendInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377407)，此函数将由指定的文件追加**LayoutFile**中的条目[ **INF 版本部分**](inf-version-section.md) INF 文件的打开到在调用期间[ **SetupOpenInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377409)。

当不再需要 INF 文件中的信息时，应用程序应调用[ **SetupCloseInfFile** ](https://msdn.microsoft.com/library/windows/desktop/aa376985)释放资源分配到在调用期间[ **SetupOpenInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377409)。

 

 





