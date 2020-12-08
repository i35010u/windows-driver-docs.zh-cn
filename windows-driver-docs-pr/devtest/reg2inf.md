---
title: Reg2inf
description: Reg2inf 是一种工具，可将注册表项转换为通用驱动程序包。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8c3a6672e724a3967b588170decc0e0f23dd426e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837303"
---
# <a name="reg2inf"></a>Reg2inf
 
驱动程序包 INF 注册表转换工具 (`reg2inf.exe`) 工具将注册表项及其值或用于实现 [**DllRegisterServer**](/windows/win32/api/olectl/nf-olectl-dllregisterserver) 例程的 COM .dll 转换为一组用于包含在驱动程序包 inf 文件中的 [INF AddReg 指令](../install/inf-addreg-directive.md) 。  此工具特别适用于将现有 [Inf RegisterDlls 指令](../install/inf-registerdlls-directive.md) 转换为 inf AddReg 指令，以便使 INF 文件成为通用文件。  有关通用 INF 文件的详细信息，请参阅 [使用通用 Inf 文件](../install/using-a-universal-inf-file.md)。
 
从 Windows 10 版本1709开始，该工具作为 WDK 10 安装的一部分提供。 例如，可以在 WDK 10 安装的 \tools 子目录中找到该文件 `c:\Program Files(x86)\Windows Kits\10\tools\` 。 

尽管 Reg2inf 尝试生成 COM 注册，但它可能不会捕获 COM 注册提供的完整注册表状态。 与往常一样，你应该检查该工具的输出的完整性和正确性，并测试结果。 

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

**注意** Reg2inf 要求完整路径长度不得超过259个字符。 

## <a name="registering-a-com-component-in-an-inf-file"></a>在 INF 文件中注册 COM 组件

以下代码片段演示了如何使用 Reg2inf 生成的 INF AddReg 语法注册简单 COM 类：

```cpp
[ComClass_AddReg]
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084},,,"Sample Class"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,,%REG_EXPAND_SZ%,"%13%\comobj.dll"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,ThreadingModel,,"Both"
```
