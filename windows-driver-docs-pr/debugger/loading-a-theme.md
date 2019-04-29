---
title: 加载主题
description: 加载主题
ms.assetid: 375b7365-6526-4282-893e-91b58a14c31f
keywords:
- 正在加载的主题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ea987d8f75448fcd40c483e2a9b9e84be203b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383337"
---
# <a name="loading-a-theme"></a>加载主题


之前加载一个主题，我们建议您清除所有工作区数据。 可以通过三种方式执行此操作：

通过使用 WinDbg 用户界面。 下**文件**菜单中，选择**清除工作区...** 选择**清除所有**在弹出窗口，然后单击**确定**。

通过删除下的注册表项**HKCU\\软件\\Microsoft\\Windbg\\工作区**。

通过运行命令**reg 删除 HKCU\\软件\\Microsoft\\Windbg**。

别忘了您的工作区的数据已清除，运行其中一个主题。 这些存储为.reg 文件的 Windows 调试工具安装在主题目录中。 运行一个主题将其设置导入注册表中，重新定义你基本的工作区。

已加载主题后，可能会更改它以更好地满足您的首选项。 一些常见的选项的更多详细信息，请参阅[自定义主题](customizing-a-theme.md)。

 

 





