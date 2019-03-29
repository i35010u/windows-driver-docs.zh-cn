---
title: 下载用于调试的 Windows 符号包
description: 此页提供有关用于调试 Windows 符号包下载。
keywords:
- 下载 Windows 调试
- WinDbg
- 下载
- 符号
- 下载符号
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2c32a3743b44db5299f0becc4f6e80320656bc51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563894"
---
# <a name="windows-symbol-packages"></a>Windows 符号程序包

符号文件使调试代码更加容易。 若要获取 Windows 符号的最简单方法是使用[Microsoft 公共符号服务器](microsoft-public-symbols.md)。 符号服务器根据需要为调试工具提供符号。 从符号服务器下载符号文件后，该文件将缓存在本地计算机上，以供快速访问。 


## <a name="symbol-package-deprecation"></a>符号包不推荐使用

> [!IMPORTANT]
> 我们不能再为 Windows 发布脱机符号包。
>
> 我们为 Windows 发布的更新的频率，使用调试的符号我们通过此页上的包发布 Windows 会快速进行过期。 
> 我们已显著改进的联机[Microsoft 符号服务器](microsoft-public-symbols.md)通过移动这是基于 Azure 的符号存储区中和符号的所有 Windows 版本和更新有可用。 
> 您可以找到更多有关这在此[博客文章](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/)。 
>
> 有关如何为未连接到 Internet 的计算机检索符号的信息，请参阅[通过 SymChk 使用清单文件](using-a-manifest-file-with-symchk.md)。

## <a name="symbol-resources-and-feedback"></a>符号的资源和反馈

若要了解有关使用符号和调试的详细信息，请参阅[符号和符号文件](symbols-and-symbol-files.md)。

有关调试问题的帮助，请参阅[调试资源](debugging-resources.md)。 

我们感兴趣有关符号的反馈。 请邮件建议或 bug 报告给[ windbgfb@microsoft.com ](mailto:windbgfb@microsoft.com)。 我们不会通过此地址提供技术支持，但是你的反馈将帮助我们规划以后对符号的更改，并使它们以后对你更有用。 

## <a name="looking-for-related-downloads"></a>查找相关下载？

- [下载 Windows 调试工具](debugger-download-tools.md)

- [下载 Windows 驱动程序工具包 (WDK)](https://developer.microsoft.com/windows/hardware/windows-driver-kit)

- [下载 Windows 评估和部署工具包 (Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)

- [下载 Windows HLK、HCK 或徽标工具包](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit)

- [下载 Windows Insider Preview 版本](https://insider.windows.com/)
