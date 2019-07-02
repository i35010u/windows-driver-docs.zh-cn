---
title: Windows 更新的脱机符号
description: 本主题介绍可以如何使用行符号关闭 Windows update。
keywords:
- 符号
- 安装程序符号
- 符号，安装程序
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f861efa47e89d5d855609589ae6b025a9c044ae
ms.sourcegitcommit: 2854c02cbe5b2c0010d0c64367cfe8dbd201d3f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67499801"
---
# <a name="offline-symbols-for-windows-update"></a>Windows 更新的脱机符号

本主题介绍如何使用脱机符号的 Windows 更新。 它描述了可用于解码无权访问 Microsoft 符号服务器的计算机上的 Windows 更新日志的过程。 

如果您发现自己无需执行此操作通常，应看到符号代理服务器设置是否可用于网络配置。 有关详细信息请参阅[SymProxy](https://docs.microsoft.com/windows-hardware/drivers/debugger/symproxy)。

下面的所有选项都要求在一台计算机可以连接到 Microsoft 符号服务器，并能够将文件复制到或从包含日志的计算机。 不能访问到符号服务器的计算机将称为*脱机*计算机和计算机有权访问作为*联机*机。

 我们建议使用 OS 内部版本每一台联机计算机以便 WU 符号缓存将生成按月和包含多个更新版本中的 WU 符号。 
 
如果你有权访问的联机计算机脱机的计算机相同的确切的补丁级别，您有两个选项：

- [选项 1：将 ETL 事件日志复制到联机状态的计算机](#ETL)

- [选项 2：将符号复制到脱机计算机](#OFFLINE)

通过运行相同的版本级别验证联机和脱机电脑`winver`或`ver`两台计算机上。

```console
C:\>ver

Microsoft Windows [Version 10.0.17134.167]
```

如果您没有使用相同的版本的联机计算机的访问权限，你将需要完成一些额外步骤才能创建 SymChk 清单文件，在本主题后面所述[选项 3:创建 SymChk 清单文件](#SYMCHK)。


## <a name="span-idetlspanspan-idetlspanoption-1-copy-the-etl-event-log-to-the-online-machine"></a><span id="etl"></span><span id="ETL"></span>选项 1:将 ETL 事件日志复制到联机状态的计算机

1. 复制所有 WindowsUpdate ETL 文件从`C:\Windows\logs\WindowsUpdate\`到计算机中联机。

2. 在联机计算机上打开 PowerShell 提示符并运行以下[Get WindowsUpdateLog](https://docs.microsoft.com/powershell/module/windowsupdate/get-windowsupdatelog?view=win10-ps) PowerShell 命令。 

   ```powershell
   Get-WindowsUpdateLog -ETLPath <path to ETLs>
   ```
   这会下载所需的日志分析的符号。


## <a name="span-idofflinespanspan-idofflinespanoption-2-copy-the-symbols-to-the-offline-machine"></a><span id="offline"></span><span id="OFFLINE"></span>选项 2:将符号复制到脱机计算机

1. 在联机计算机上打开 PowerShell 提示符并运行"Get WindowsUpdateLog"。 这会缓存所需的日志分析的符号。

2. %Temp%\WindowsUpdateLog\SymCache 中的所有文件复制到在联机计算机从`%temp%\WindowsUpdateLog\SymCache`脱机计算机上。

3. 脱机计算机上打开 PowerShell 提示符并运行"Get-WindowsUpdateLog"来分析日志。


## <a name="span-idsymchkspanspan-idsymchkspanoption-3-create-a-symchk-manifest-file"></a><span id="symchk"></span><span id="SYMCHK"></span>选项 3:创建 SymChk 清单文件

1.  对于脱机的计算机，请按照步骤[清单文件中使用 SymChk](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-a-manifest-file-with-symchk) system32 目录中创建这些文件的清单：

    ```console
    storewuauth.dll
    wuapi.dll
    wuauclt.exe
    wuaueng.dll
    wuautoappupdate.dll
    wuuhext.dll
    wuuhmobile.dll
    ```

2.  复制到联机计算机清单。

3.  与清单文件中，使用 SymChk 您联机的电脑的本地下载符号。 

4.  将复制的文件夹和您传递到 SymChk %temp%\WindowsUpdateLog\SymCache 你脱机的 PC 的符号。
 
5. 脱机计算机上打开 PowerShell 提示符并运行"Get-WindowsUpdateLog"来分析日志。

 



## <a name="see-also"></a>请参阅

[使用符号服务器](using-a-symbol-server.md)。

[符号路径](symbol-path.md) 

[访问用于调试的符号](accessing-symbols-for-debugging.md)

[符号进行调试时的问题](symbol-problems-while-debugging.md)
 





