---
title: 跟踪托管的对象格式 (MOF) 文件
description: 跟踪托管的对象格式 (MOF) 文件
ms.assetid: e0ef452b-042d-42d0-be0f-b36e7bf47285
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c59746b7db6531087f94418e8ebefb17a612a5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519531"
---
# <a name="trace-managed-object-format-mof-file"></a>跟踪托管的对象格式 (MOF) 文件


跟踪[托管的对象格式](https://go.microsoft.com/fwlink/p/?linkid=74565)(MOF) 文件是文本文件，其中包含每个控件 GUID[跟踪提供程序](trace-provider.md)PDB 文件中表示。 MOF 文件的名称是跟踪生成者、.mof 文件扩展名的模块名称。

[Tracepdb](tracepdb.md)并[BinPlace](binplace.md)时他们创建的跟踪消息格式 (.tmf) 文件中的 PDB 文件的格式设置操作说明，为每个跟踪提供程序创建的 MOF 文件。

跟踪 MOF 文件还包含以下信息：

-   PDB 文件的路径和文件名称。

-   日期和 PDB 文件的创建时间。

-   为每个跟踪提供程序的控件的 GUID。

-   跟踪提供程序定义的跟踪标志。

Logman 和 Perfmon 可以使用 MOF 文件以查找每个提供程序的跟踪标志。 为控件的跟踪提供程序的 GUID 的快速参考，可以使用 MOF 文件。
