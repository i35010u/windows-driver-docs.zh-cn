---
title: Windows 更新的脱机符号
description: 本主题介绍如何处理 Windows 更新的 off 行符号。
keywords:
- symbols
- 设置，符号
- 符号，安装程序
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ee63ce37645064ef43c49317f71edf5b536f0118
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534296"
---
# <a name="offline-symbols-for-windows-update"></a>Windows 更新的脱机符号

本主题介绍如何处理 Windows 更新的脱机符号。 本文介绍了一个过程，该过程可用于对无法访问 Microsoft 符号服务器的计算机上的 Windows 更新日志进行解码。 

如果你发现自己需要经常执行此操作，则应看到设置符号代理服务器是否适用于你的网络配置。 有关详细信息，请参阅[SymProxy](symproxy.md)。

下面的所有选项都要求您具有一个可以连接到 Microsoft 的符号服务器的计算机，并能够将文件复制到具有日志的计算机或从中复制文件。 无权访问符号服务器的计算机将称为 "*脱机*计算机"，并且具有作为*联机*计算机的访问权限的计算机。

 建议对每个 OS 版本使用单个联机计算机，使 WU 符号缓存按月生成并包含来自多个更新版本的 WU 符号。 
 
如果你有权访问与脱机计算机具有相同修补程序级别的联机计算机，你有两种选择：

- [选项1：将 ETL 事件日志复制到联机计算机](#ETL)

- [选项2：将符号复制到脱机计算机](#OFFLINE)

在 `winver` `ver` 两台计算机上运行或，验证联机和脱机 pc 的版本级别是否相同。

```console
C:\>ver

Microsoft Windows [Version 10.0.17134.167]
```

如果你没有访问具有相同版本的联机计算机的权限，则需要完成一些额外的步骤来创建 SymChk 清单文件，如本主题后面的[选项3：创建 SymChk 清单文件](#SYMCHK)中所述。


## <a name="span-idetlspanspan-idetlspanoption-1-copy-the-etl-event-log-to-the-online-machine"></a><span id="etl"></span><span id="ETL"></span>选项1：将 ETL 事件日志复制到联机计算机

1. 将所有 Windowsupdate.log ETL 文件从复制 `C:\Windows\logs\WindowsUpdate\` 到您的联机计算机。

2. 在联机计算机上，打开 PowerShell 提示符并运行以下[WindowsUpdateLog](https://docs.microsoft.com/powershell/module/windowsupdate/get-windowsupdatelog?view=win10-ps) PowerShell 命令。 

   ```powershell
   Get-WindowsUpdateLog -ETLPath <path to ETLs>
   ```
   这将下载日志分析所需的符号。


## <a name="span-idofflinespanspan-idofflinespanoption-2-copy-the-symbols-to-the-offline-machine"></a><span id="offline"></span><span id="OFFLINE"></span>选项2：将符号复制到脱机计算机

1. 在联机计算机上，打开 PowerShell 提示符并运行 "WindowsUpdateLog"。 这会缓存日志分析所需的符号。

2. 将%temp%\WindowsUpdateLog\SymCache 中的所有文件从联机计算机复制到 `%temp%\WindowsUpdateLog\SymCache` 脱机计算机上的。

3. 在脱机计算机上，打开 PowerShell 提示符并运行 "WindowsUpdateLog" 以分析日志。


## <a name="span-idsymchkspanspan-idsymchkspanoption-3-create-a-symchk-manifest-file"></a><span id="symchk"></span><span id="SYMCHK"></span>选项3：创建 SymChk 清单文件

1.  在脱机计算机上，按照[使用带有 SymChk 的清单文件](using-a-manifest-file-with-symchk.md)中的步骤为 system32 目录中的这些文件创建清单：

    ```console
    storewuauth.dll
    wuapi.dll
    wuauclt.exe
    wuaueng.dll
    wuautoappupdate.dll
    wuuhext.dll
    wuuhmobile.dll
    ```

2.  将清单复制到您的联机计算机。

3.  使用清单文件，使用 SymChk 将符号下载到本地 PC。 

4.  将您传递给 SymChk 的文件夹和符号复制到您的脱机 PC 上的%temp%\WindowsUpdateLog\SymCache。
 
5. 在脱机计算机上，打开 PowerShell 提示符并运行 "WindowsUpdateLog" 以分析日志。

 



## <a name="see-also"></a>另请参阅

[使用符号服务器](using-a-symbol-server.md)。

[符号路径](symbol-path.md) 

[访问调试符号](accessing-symbols-for-debugging.md)

[调试时的符号问题](symbol-problems-while-debugging.md)
 





