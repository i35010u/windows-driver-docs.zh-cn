---
title: 安装 SymProxy
description: 安装 SymProxy
ms.assetid: 63633de7-d254-415d-bf06-c0e81bd03e74
keywords:
- SymProxy 安装
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 378343416a1cc61c49b4353a97794154ccd58f0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371646"
---
# <a name="installing-symproxy"></a>安装 SymProxy


## <a name="span-idsummaryofinstallationtasksspanspan-idsummaryofinstallationtasksspanspan-idsummaryofinstallationtasksspansummary-of-installation-tasks"></a><span id="Summary_of_installation_tasks"></span><span id="summary_of_installation_tasks"></span><span id="SUMMARY_OF_INSTALLATION_TASKS"></span>安装任务的摘要


下面概述了用于安装和配置 SymProxy 的任务。

-   SymProxy 文件需要复制到 %WINDIR%\\system32\\iis inetsrv 文件夹。 下面将讨论此任务。

-   需要为 SymProxy 配置注册表。 有关详细信息请参阅[配置注册表](configuring-the-registry.md)。

-   清单需要注册为性能计数器和 ETW 事件和事件日志需要进行配置。

-   需要配置 IIS。 有关详细信息，请参阅[选择网络安全凭据](choosing-network-security-credentials.md)并[配置 IIS 以实现 SymProxy](configuring-iis-for-symproxy.md)。

可以使用 Install.cmd 文件自动完成这些步骤。 有关详细信息，请参阅[SymProxy Automated Installation](symproxy-automated-installation.md)。

## <a name="span-idcopythesymproxyfilestoiisspanspan-idcopythesymproxyfilestoiisspanspan-idcopythesymproxyfilestoiisspancopy-the-symproxy-files-to-iis"></a><span id="Copy_the_SymProxy_files_to_IIS"></span><span id="copy_the_symproxy_files_to_iis"></span><span id="COPY_THE_SYMPROXY_FILES_TO_IIS"></span>将 SymProxy 文件复制到 IIS


SymProxy 文件包含在 Windows 驱动程序工具包调试器目录中。 例如，这是 Windows 10 套件的 64 位文件的位置。 C:\\Program Files (x86)\\Windows 工具包\\10\\调试器\\x64\\symproxy。

若要在服务器上安装 SymProxy，复制 symproxy.dll、 symsrv.dll 和 symproxy.man 到 %WINDIR%\\system32\\inetsrv。

为了防止访问 Microsoft 符号存储区中可能会出现的问题，创建空白文件，名为 %WINDIR%\\system32\\inetsrv\\symsrv.yes。 此文件的内容并不重要。 当存在 symsrv.yes 文件时，它会自动接受 EULA 以供 Microsoft 公共符号存储区。

请注意，通常情况下随一起安装的 IIS 和 Windows server 如"Baltimore CyberTrust Root"用于对上游提供程序的 HTTPS/TLS 通信，它们必须位于受信任的根证书存储 SymProxy 的计算机上正在运行。 有关 SSL 问题疑难解答的一般信息，请参阅[故障排除 SSL 相关问题 （服务器证书）](https://docs.microsoft.com/iis/troubleshoot/security-issues/troubleshooting-ssl-related-issues-server-certificate)。

 

 





