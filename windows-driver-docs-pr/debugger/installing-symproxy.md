---
title: 安装 SymProxy
description: 安装 SymProxy
ms.assetid: 63633de7-d254-415d-bf06-c0e81bd03e74
keywords:
- SymProxy，安装
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: c6dd0cf6482859cc70869e434079e54245c5dc09
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216660"
---
# <a name="installing-symproxy"></a>安装 SymProxy


## <a name="span-idsummary_of_installation_tasksspanspan-idsummary_of_installation_tasksspanspan-idsummary_of_installation_tasksspansummary-of-installation-tasks"></a><span id="Summary_of_installation_tasks"></span><span id="summary_of_installation_tasks"></span><span id="SUMMARY_OF_INSTALLATION_TASKS"></span>安装任务摘要


下面总结了用于安装和配置 SymProxy 的任务。

-   需要将 SymProxy 文件复制到 IIS 的% WINDIR% \\ system32 \\ inetsrv 文件夹。 此任务如下所述。

-   需要为 SymProxy 配置注册表。 有关详细信息，请参阅 [配置注册表](configuring-the-registry.md)。

-   需要将清单注册为性能计数器和 ETW 事件，并且需要配置事件日志。

-   需要配置 IIS。 有关详细信息，请参阅 [选择网络安全凭据](choosing-network-security-credentials.md) 和 [为 SymProxy 配置 IIS](configuring-iis-for-symproxy.md)。

可以使用 Install .cmd 文件自动执行这些步骤。 有关详细信息，请参阅 [SymProxy 自动安装](symproxy-automated-installation.md)。

## <a name="span-idcopy_the_symproxy_files_to_iisspanspan-idcopy_the_symproxy_files_to_iisspanspan-idcopy_the_symproxy_files_to_iisspancopy-the-symproxy-files-to-iis"></a><span id="Copy_the_SymProxy_files_to_IIS"></span><span id="copy_the_symproxy_files_to_iis"></span><span id="COPY_THE_SYMPROXY_FILES_TO_IIS"></span>将 SymProxy 文件复制到 IIS


SymProxy 文件包含在 Windows 驱动程序工具包的 "调试程序" 目录中。 例如，这是适用于 Windows 10 工具包的64位文件的位置。 C： \\ Program Files (x86) \\ Windows 工具包 \\ 10 \\ 调试器 \\ x64 \\ symproxy。

若要在服务器上安装 SymProxy，请将 symproxy.dll、symsrv.dll 和 SymProxy 复制到% WINDIR% \\ system32 \\ inetsrv。

若要防止在访问 Microsoft 符号存储时出现问题，请创建名为% WINDIR% \\ system32 inetsrv symsrv 的空白 \\ 文件 \\ 。 此文件的内容并不重要。 如果存在 symsrv 文件，它会自动接受 Microsoft 公共符号存储的 EULA。

请注意，通常与 IIS 和 Windows server 一起安装的证书（如 "巴尔的摩 CyberTrust Root"）用于与上游提供程序的 HTTPS/TLS 通信，它们需要位于运行 SymProxy 的计算机上的受信任根存储区中。 有关解决 SSL 问题的常规信息，请参阅 [排查 ssl 相关问题 (服务器证书) ](/iis/troubleshoot/security-issues/troubleshooting-ssl-related-issues-server-certificate)。

 

