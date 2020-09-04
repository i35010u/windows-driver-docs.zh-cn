---
title: 下载用于调试的 Windows 符号包
description: 本页提供用于调试的 Windows 符号程序包下载。
keywords:
- Windows 调试工具下载
- WinDbg
- 下载
- 符号
- 下载符号
ms.date: 04/26/2018
ms.localizationpriority: High
ms.openlocfilehash: 29c000e8f192c6e61603252dc24486156168380e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211197"
---
# <a name="windows-symbol-packages"></a>Windows 符号程序包

符号文件使调试代码更加容易。 获取 Windows 符号的最简单方法是使用 [Microsoft 公共符号服务器](microsoft-public-symbols.md)。 符号服务器根据需要为调试工具提供符号。 从符号服务器下载符号文件后，该文件将缓存在本地计算机上，以供快速访问。 

## <a name="symbol-package-deprecation"></a>符号包弃用

> [!IMPORTANT]
> 我们不再发布用于 Windows 的脱机符号包。
>
> 随着我们发布 Windows 更新的节奏，通过此页上的程序包发布的 Windows 调试符号很快就会过时。
> 我们已对联机 [Microsoft 符号服务器](microsoft-public-symbols.md)进行了重大改进，移动此内容形成一个基于 Azure 的符号存储，并且其中可提供所有 Windows 版本和更新的符号。 
> 可以在此[博客文章](/archive/blogs/windbg/update-on-microsofts-symbol-server)中找到有关此内容的详细信息。
>
> 有关如何为未连接到 Internet 的计算机检索符号的信息，请参阅[通过 SymChk 使用清单文件](using-a-manifest-file-with-symchk.md)。

## <a name="symbol-resources-and-feedback"></a>符号资源和反馈

若要了解有关使用符号和调试的详细信息，请参阅[符号和符号文件](symbols-and-symbol-files.md)。

有关调试问题的帮助，请参阅[调试资源](debugging-resources.md)。

我们对有关符号的反馈非常感兴趣。 请通过邮件将建议或错误报告发送至 [windbgfb@microsoft.com](mailto:windbgfb@microsoft.com)。 我们不会通过此地址提供技术支持，但是你的反馈将帮助我们规划以后对符号的更改，并使它们以后对你更有用。

## <a name="looking-for-related-downloads"></a>查找相关下载？

- [下载 Windows 调试工具](debugger-download-tools.md)

- [下载 Windows 驱动程序工具包 (WDK)](../download-the-wdk.md)

- [下载 Windows 评估和部署工具包 (Windows ADK)](/windows-hardware/get-started/adk-install)

- [下载 Windows HLK、HCK 或徽标工具包](/windows-hardware/test/hlk/windows-hardware-lab-kit)

- [下载 Windows Insider Preview 版本](https://insider.windows.com/)