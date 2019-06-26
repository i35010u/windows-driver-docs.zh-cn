---
title: 网络 INF 文件中的 ControlFlags 节
description: 网络 INF 文件中的 ControlFlags 节
ms.assetid: 384e56e3-8a64-4b47-ae9c-e9973733c7e7
keywords:
- INF 文件 WDK 网络，ControlFlags 部分
- 可使用网络 INF 文件 WDK，ControlFlags 部分
- ControlFlags 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65cdae07b06b1b4edfa8d2eacf85c25fa280024f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374943"
---
# <a name="controlflags-section-in-a-network-inf-file"></a>网络 INF 文件中的 ControlFlags 节





一个**ControlFlags**网络 INF 文件中的部分基于泛型[ **INF ControlFlags 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)。

**ControlFlags**网络 INF 文件中的部分通常具有一个或多个**ExcludeFromSelect**条目。 每个**ExcludeFromSelect**条目指定将不会显示给最终用户手动安装过程中选择的网络组件。

**ControlFlags**网络 INF 文件中的部分必须包含**ExcludeFromSelect**项，为每个插适配器的安装，并且应添加任何软件组件以编程方式而不是手动用户。

不符合即插的适配器必须由用户手动添加，并因此不应列出在*ControlFlags*部分。 例如，非即插即用 ISA 适配器和 EISA 适配器必须手动添加用户。 请注意，Windows XP 和更高版本操作系统不支持非即插即用 ISA 适配器和 EISA 适配器。

**请注意**   **ExcludeFromSelect**条目执行不同的功能比 NCF\_HIDDEN 值**特征**中的条目*DDInstall*部分。 有关详细信息，请参阅[DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

 

**ExcludeFromSelect**条目可防止适配器或软件组件列出**安装选择组件**对话框。 适配器或组件，但是，仍然可以列在**连接**对话框。 NCF\_HIDDEN 值阻止适配器或组件显示的用户界面中，任何部分中包括**连接**对话框。

 

 





