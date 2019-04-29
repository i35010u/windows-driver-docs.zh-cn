---
title: Windows 驱动程序目标
description: WindowsDriver.Common.targets、 WindowsDriver.masm.targets 和 WindowsDriver.arm.targets 文件提供构建一个驱动程序所需的目标。
ms.assetid: 9D04792B-2736-4871-A53E-6B90509133A7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc8363e8df2f936b7b9fcad0b31579b86d88abda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379116"
---
# <a name="windows-driver-targets"></a>Windows 驱动程序目标


WindowsDriver.Common.targets、 WindowsDriver.masm.targets 和 WindowsDriver.arm.targets 文件提供构建一个驱动程序所需的目标。

WindowsDriver.masm.targets 和 WindowsDriver.arm.targets 定义专门用于构建程序集文件的目标。

这些目标而无需直接修改这些扩展的 Cpp 目标。 MSBuild 提供了一种机制，独立于原始项目，以便插入行为，同时保留用于保证排序扩展之间的原始机制的结构。

 

 





