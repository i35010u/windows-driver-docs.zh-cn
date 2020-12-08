---
title: 加载主题
description: 加载主题
keywords:
- 主题，加载
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9433131f45be973cd1f2df20e8d5486980413fcd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838169"
---
# <a name="loading-a-theme"></a>加载主题


在加载主题之前，我们建议您清除所有工作区数据。 可以通过三种方式完成此操作：

使用 WinDbg 用户界面。 在 " **文件** " 菜单下，选择 " **清除工作区 ...** "在弹出窗口中选择 " **全部清除** "，然后单击 **"确定"**。

删除 **HKCU \\ Software \\ Microsoft \\ Windbg \\ 工作区** 下的注册表项。

通过运行命令 **reg DELETE HKCU \\ Software \\ Microsoft \\ Windbg**。

清除所有工作区数据后，运行其中一个主题。 这些文件在用于 Windows 的调试工具的 "主题" 目录中作为 .reg 文件存储。 运行主题会将其设置导入注册表，并重新定义基本工作区。

加载主题后，您可以对其进行更改，使其更适合您的偏好。 有关某些常见选项的更多详细信息，请参阅 [自定义主题](customizing-a-theme.md)。

 

 





