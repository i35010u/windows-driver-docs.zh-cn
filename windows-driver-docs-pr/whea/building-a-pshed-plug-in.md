---
title: 构建 PSHED 插件
description: 构建 PSHED 插件
ms.assetid: 2d4dc052-af8b-4ee1-a8e7-4dbbb3817616
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9b63ef90318f0b2d69feb1ec0625b241dc56cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542426"
---
# <a name="building-a-pshed-plug-in"></a>构建 PSHED 插件


PSHED 插件生成的只不过将链接到内核和硬件抽象层 (HAL)，除了 PSHED 插件必须显式链接到使用像任何其他 Windows 驱动程序模型 (WDM) 设备驱动程序 WDK *Pshed.lib*.

**请注意**  从 Windows 7 开始，各种 Windows 硬件错误体系结构 (WHEA) 数据类型已重命名从早期版本的 WDK。 有关这些更改的详细信息，请参阅[重命名 WHEA 数据类型](renamed-whea-data-types.md)。 如果您计划构建 Windows 7 或更高版本的 WDK 插件现有 PSHED，您仍可以使用以前的 WHEA 数据类型名称。 若要执行此操作，添加以下信息*源*用于生成该插件的文件： `C_DEFINES = $(C_DEFINES) /DWHEA_DOWNLEVEL_TYPE_NAMES`

 

 

 




