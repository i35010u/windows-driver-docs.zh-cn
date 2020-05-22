---
title: 跟踪托管对象格式 (MOF) 文件
description: 跟踪托管对象格式 (MOF) 文件
ms.assetid: e0ef452b-042d-42d0-be0f-b36e7bf47285
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0de160d0af0595a07fe826cf0f4a859791ab66d7
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769649"
---
# <a name="trace-managed-object-format-mof-file"></a>跟踪托管对象格式 (MOF) 文件


跟踪[托管对象格式](https://docs.microsoft.com/windows/win32/wmisdk/managed-object-format--mof-)（MOF）文件是一个文本文件，该文件包含 PDB 文件中表示的每个[跟踪提供程序](trace-provider.md)的控件 GUID。 MOF 文件的名称为跟踪制造者的模块名称，后跟 MOF 文件扩展名。

[Tracepdb](tracepdb.md)和[BINPLACE](binplace.md)在从 PDB 文件中的格式说明创建跟踪消息格式（. tmf）文件时，为每个跟踪提供程序创建 MOF 文件。

跟踪 MOF 文件还包含以下信息：

-   PDB 文件的路径和文件名。

-   创建 PDB 文件的日期和时间。

-   每个跟踪提供程序的控件 GUID。

-   跟踪提供程序定义的跟踪标志。

Logman 和 Perfmon 可以使用 MOF 文件查找每个提供程序的跟踪标志。 您可以使用 MOF 文件作为跟踪提供程序的控件 GUID 的快速参考。
