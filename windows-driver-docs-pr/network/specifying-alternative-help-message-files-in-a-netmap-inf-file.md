---
title: Netmap.inf 文件中指定备用的帮助消息文件
description: Netmap.inf 文件中指定备用的帮助消息文件
ms.assetid: 66ab7124-803a-4497-b5e0-98b47006dfb6
keywords:
- 网络组件升级，WDK，netmap.inf 文件
- 升级网络组件 WDK，netmap.inf 文件
- netmap.inf 文件 WDK
- 设备 Id WDK netmap.inf
- 帮助消息文件 WDK netmap.inf
- 备用的帮助消息文件 WDK netmap.inf
- 供应商提供的文件 WDK netmap.inf 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90811d5ba23b3e3771e9c98461bb720fee3781a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520172"
---
# <a name="specifying-alternative-help-message-files-in-a-netmapinf-file"></a>Netmap.inf 文件中指定备用的帮助消息文件





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

如果 NetSetup 无法在任何 netmap.inf 文件中查找设备 ID 映射的网络组件，它列出了在向导的兼容性报告页上的该组件。 与每个此类组件是一个帮助消息文件。

默认情况下显示中包含的帮助消息 NetSetup \\winntupg\\unsupmsg.txt 文件或 HTML 浏览器安装在系统上，在\\winntupg\\unsupmsg.htm 文件。 （可选） 可以提供自定义消息文件，以替代 unsupmsg.txt 和 unsupmsg.txt 消息文件。 例如，如果供应商提供了只有某些及其网络组件提供升级支持，供应商无法提供指示没有为某些组件提供升级支持的自定义帮助消息文件。

一个可选**OemUpgradeHelpFiles** netmap.inf 文件中的节指定一个或多个自定义的帮助消息文件。 在本部分中的每个条目具有以下格式：

*postupgrade ID* = *文本名称*， *htm 文件*

其中：

*postupgrade ID*是 Windows 2000 或更高版本的设备 ID 的网络组件

*文本名称*是路径和文本版本的自定义的帮助消息文件的名称

*htm 文件*是路径和名称的 HTML 版本的自定义的帮助消息文件。

如果在未指定完整路径名称*文本名称*或*htm 文件*，指定的路径附加到 i386 目录中--例如： \\i386\\mydirectory\\myfile.txt。

下面的示例 netmap.inf 文件的包含**OemUpgradeHelpFiles**部分。

```INF
[Version]
signature="$WindowsNT$

[OemNetProtocols]
Protocol1=Protoco1_2000
Protocol2=Protocol2_2000

[OemUpgradeSupport]
Protocol1=NotSupported
Protocol2=abc_upgrade.dll, abc.inf

[OemUpgradeHelpFiles]
Protoco11=helpmsg.txt, helpmsg.htm
```

尽管此示例 netmap.inf 文件不提供升级支持 Protocol1，它为 Protocol1 中提供的设备 ID 映射**OemNetProtocols**部分。 此映射指定 Protocol1 Windows 2000 设备 ID。 Windows 2000 设备 ID 是需要将自定义帮助消息文件与某个网络组件相关联。

请注意，在关键字**NotSupported**分配给在 Protocol1 **OemUpgradeHelpFiles**部分。 此关键字指示无需加载 DLL 升级 Protocol1 的迁移。

在中**OemUpgradeHelpFiles**部分中的上一示例中，Protoco11=helpmsg.txt helpmsg.htm 条目为 Protocol1 指定两个自定义的帮助消息文件。 例如，在这些文件中包含的自定义帮助消息可能指示供应商不支持 Protocol1 升级，并且用户必须单独升级 Protocol1 到 Protocol2 然后再尝试升级到 Windows 2000 或更高版本的系统。

 

 





