---
title: 跟踪托管对象格式 (MOF) 文件
description: 跟踪托管对象格式 (MOF) 文件
ms.assetid: e0ef452b-042d-42d0-be0f-b36e7bf47285
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 340e3ff2ff64de4021847bdf67547e7362785b41
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383321"
---
# <a name="trace-managed-object-format-mof-file"></a>跟踪托管对象格式 (MOF) 文件


MOF) 文件 (的跟踪 [托管对象格式](/windows/win32/wmisdk/managed-object-format--mof-) 是文本文件，其中包含 PDB 文件中表示的每个 [跟踪提供程序](trace-provider.md) 的控件 GUID。 MOF 文件的名称为跟踪制造者的模块名称，后跟 MOF 文件扩展名。

[Tracepdb](tracepdb.md) 和 [BinPlace](binplace.md) 创建跟踪消息格式时，将为每个跟踪提供程序创建一个 MOF 文件 (. tmf) 文件中的格式说明。

跟踪 MOF 文件还包含以下信息：

-   PDB 文件的路径和文件名。

-   创建 PDB 文件的日期和时间。

-   每个跟踪提供程序的控件 GUID。

-   跟踪提供程序定义的跟踪标志。

Logman 和 Perfmon 可以使用 MOF 文件查找每个提供程序的跟踪标志。 您可以使用 MOF 文件作为跟踪提供程序的控件 GUID 的快速参考。