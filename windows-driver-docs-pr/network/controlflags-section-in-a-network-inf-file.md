---
title: 网络 INF 文件中的 ControlFlags 节
description: 网络 INF 文件中的 ControlFlags 节
keywords:
- INF 文件 WDK network，ControlFlags 部分
- 网络 INF 文件 WDK，ControlFlags 部分
- ControlFlags 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b3adb332890e71e6efaf7552aae95625c836284
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813693"
---
# <a name="controlflags-section-in-a-network-inf-file"></a>网络 INF 文件中的 ControlFlags 节





网络 INF 文件中的 **ControlFlags** 部分基于通用 [**INF ControlFlags 部分**](../install/inf-controlflags-section.md)。

网络 INF 文件中的 **ControlFlags** 部分通常包含一个或多个 **ExcludeFromSelect** 条目。 每个 **ExcludeFromSelect** 条目指定一个网络组件，该组件不会在手动安装过程中作为选项显示给最终用户。

网络 INF 文件中的 **ControlFlags** 部分必须包含用于安装的每个即插即用适配器的 **ExcludeFromSelect** 条目，以及应以编程方式而不是由用户手动添加的任何软件组件。

与即插即用不兼容的适配器必须由用户手动添加，因此不应在 *ControlFlags* 节中列出。 例如，用户必须手动添加非 PnP ISA 适配器和 EISA 适配器。 请注意，Windows XP 和更高版本的操作系统不支持非 PnP ISA 适配器和 EISA 适配器。

**注意** **ExcludeFromSelect** 项执行的功能与 \_ *DDInstall* 节中的 "**特性**" 项的 NCF 隐藏值不同。 有关详细信息，请参阅 [DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

 

**ExcludeFromSelect** 条目阻止在 "**选择要安装的组件**" 对话框中列出适配器或软件组件。 但是，适配器或组件仍可以在 " **连接** " 对话框中列出。 NCF \_ 隐藏值可防止适配器或组件显示在用户界面的任何部分（包括 " **连接** " 对话框）中。

 

