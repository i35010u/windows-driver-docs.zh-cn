---
title: Reg2inf
description: Reg2inf 是一种工具，将注册表项以使驱动程序包的通用转换。
ms.assetid: e43a137e-c08a-4715-84f7-32cda67399e3
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 788a4a0288461f79e1f26a1ea3a128f643bd5e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356387"
---
# <a name="reg2inf"></a>Reg2inf
 
驱动程序程序包 INF 注册表转换工具 (`reg2inf.exe`) 工具将为注册表项和它的值或 COM.dll 实现[ **DllRegisterServer** ](https://docs.microsoft.com/windows/desktop/api/olectl/nf-olectl-dllregisterserver)成一组例程[INF AddReg 指令](../install/inf-addreg-directive.md)以便包括到驱动程序包 INF 文件。  此工具是用于转换现有特别有用[INF RegisterDlls 指令](../install/inf-registerdlls-directive.md)到 INF AddReg 指令以使文件通用 INF。  有关通用 INF 文件的详细信息，请参阅[使用通用 INF 文件](../install/using-a-universal-inf-file.md)。
 
从 Windows 10 1709年版开始，此工具附带作为 WDK 10 安装的一部分。 您可以找到它在 WDK 10 安装，\tools 子目录例如`c:\Program Files(x86)\Windows Kits\10\tools\`。 

虽然 Reg2inf 尝试生成 COM 注册，它可能会捕获 COM 注册提供完整注册状态。 与往常一样，应检查的完整性和正确性，该工具的输出和测试的结果。 

## <a name="running-reg2inf-from-the-command-line"></a>从命令行运行 Reg2inf 
 
本部分列出了 Reg2inf 的命令行选项。

```
USAGE: reg2inf.exe [/key <path> | /dll <filename>] [/targetkey <path>]

/key <registry key path>
    Process a specific registry key, e.g.: reg2inf /key HKEY_LOCAL_MACHINE\SOFTWARE\Fabrikam
/dll <module filename>
    Process a COM DLL module that implements DllRegisterServer entrypoint, typically called by regsvr32 or legacy INF RegisterDlls directive in order to register COM class under HKEY_CLASSES_ROOT, e.g.: reg2inf /dll %SystemRoot%\System32\fabkobj.dll
/targetkey <registry key path>
    Remap target registry key to be under a different base key path, e.g.: reg2inf /key HKLM\SYSTEM\Temp /targetkey HKR\Parameters
```

**请注意**Reg2inf 要求的完整路径长度不能超过 259 个字符。 
