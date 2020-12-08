---
title: 在 Netmap.inf 文件中指定备用帮助消息文件
description: 在 Netmap.inf 文件中指定备用帮助消息文件
keywords:
- 网络组件升级 WDK，netmap .inf 文件
- 升级网络组件 WDK，netmap .inf 文件
- netmap 文件 WDK
- 设备 Id WDK netmap
- 帮助消息文件 WDK netmap
- 备用帮助消息文件 WDK netmap
- 供应商提供的文件 WDK netmap 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 107efdbf568f21010181c85bd36639f46f05b48d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790469"
---
# <a name="specifying-alternative-help-message-files-in-a-netmapinf-file"></a>在 Netmap.inf 文件中指定备用帮助消息文件





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

如果 NetSetup 在任何 netmap 文件中找不到网络组件的设备 ID 映射，它将在向导的 "兼容性报告" 页上列出此组件。 与每个这样的组件相关联的是帮助消息文件。

默认情况下，NetSetup 显示包含在 winntupgunsupmsg.txt 文件中的帮助消息 \\ \\ ，或者，如果在系统上安装了 HTML 浏览器，则在 \\ winntupg \\unsupmsg.htm 文件中。 你可以选择提供一个自定义消息文件，用于重写 unsupmsg.txt 和 unsupmsg.txt 消息文件。 例如，如果某个供应商只为其某些网络组件提供升级支持，则该供应商可能会提供一个自定义帮助消息文件，指出对于某些组件，不提供升级支持。

Netmap 文件中的可选 **OemUpgradeHelpFiles** 部分指定一个或多个自定义帮助消息文件。 本节中的每个条目都具有以下格式：

*postupgrade-ID*  = *文本名称*、 *.htm 文件*

其中：

*postupgrade* 是网络组件的 Windows 2000 或更高版本设备 id

*text-name* 是自定义帮助消息文件的文本版本的路径和名称

*htm-file* 是自定义帮助消息文件的 HTML 版本的路径和名称。

如果未在 *文本名称* 或 *htm 文件* 中指定完整路径名称，则会将指定的路径追加到 i386 目录，例如： \\ i386 \\ mydirectory \\myfile.txt。

下面的 netmap 文件示例包含一个 **OemUpgradeHelpFiles** 部分。

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

尽管此示例 netmap 文件未提供对 Protocol1 的升级支持，但它为 **OemNetProtocols** 部分中的 Protocol1 提供了设备 ID 映射。 此映射为 Protocol1 指定 Windows 2000 设备 ID。 需要 Windows 2000 设备 ID 才能将自定义帮助消息文件与网络组件相关联。

请注意，关键字 **NotSupported** 分配给 **OemUpgradeHelpFiles** 节中的 Protocol1。 此关键字表示无需加载迁移 DLL 即可升级 Protocol1。

在上一示例的 **OemUpgradeHelpFiles** 节中，Protoco11 =helpmsg.txt，helpmsg.htm 条目为 Protocol1 指定了两个自定义帮助消息文件。 这些文件中包含的自定义帮助消息可能表明，供应商不支持 Protocol1 的升级，并且用户必须先将 Protocol1 升级到 Protocol2，然后再尝试将系统升级到 Windows 2000 或更高版本。

 

 





