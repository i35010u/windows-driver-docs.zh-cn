---
title: 启动选项标识符
description: 描述启动选项标识符
ms.assetid: bd0caf3f-bb35-4242-a10a-4efa91a21797
keywords:
- Windows 的引导选项
- 标识符
- default
- WDK 启动选项
ms.date: 04/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 472167b0023469065200a42dac3d0fc0a26e1522
ms.sourcegitcommit: ff586f2b9ef79af53e3317973f087eee7babf083
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "64402107"
---
# <a name="boot-options-identifiers"></a>启动选项标识符

很多 bcdedit 命令需要标识符。 标识符唯一标识启动设置存储区中包含的条目。 

使用 bcdedit /enum 显示标识符。

```console
C:\>bcdedit /enum

Windows Boot Manager
--------------------
identifier              {bootmgr}

...

Windows Boot Loader
-------------------
identifier              {current}

```

由已知的标识符，可以标识多个条目。 如果条目都有一个已知的标识符，bcdedit 将显示其输出中除非您使用 /v 命令行开关。 有关详细信息，运行"bcdedit /？ /v".

通常使用常见已知的标识符：

| 标识符           | 描述
|-----------------------|----------------------------------------------------------------------|
|    {default}          |     指定一个虚拟的标识符，对应于启动管理器默认应用程序条目。 | 
|    {current}          |     指定一个虚拟的标识符，对应于当前正在运行的操作系统的操作系统启动应用程序项目。 |
|    {bootmgr}          |     指定的 Windows 启动管理器应用程序项目。 |

这些常见已知的标识符可以由任何启动应用程序项继承：

| 标识符           | 描述
|-----------------------|----------------------------------------------------------------------|
|    {globalsettings}    |    包含的所有启动应用程序条目应都继承的全局设置的集合。 |
|   {bootloadersettings} |   包含的所有启动加载程序应用程序条目应都继承的全局设置的集合。 |

这些已知的标识符也已可供使用：

| 标识符           | 描述
|-----------------------|----------------------------------------------------------------------|
|    {dbgsettings}       |    包含全局调试器设置可继承的任何启动应用程序条目。 |
|    {hypervisorsettings} |   包含可以由任何 OS 加载程序项继承的虚拟机管理程序设置。 |
|    {emssettings}       |  包含全局紧急管理服务设置由继承的任何启动应用程序条目。 |
|    {resumeloadersettings} | 包含集合的全局设置应继承的所有 Windows 恢复从休眠状态的应用程序条目。 |
|    {badmemory}         |    包含全局 RAM 缺陷列表由继承的任何启动应用程序条目。 |
|   {memdiag}           |    指定内存诊断应用程序条目。 |
|    {ramdiskoptions}    |   包含所需的 RAM 磁盘设备的启动管理器的其他选项。 |

与早期版本的 Windows 使用这些已知的标识符：

| 标识符           | 描述
|-----------------------|----------------------------------------------------------------------|
|    {ntldr}            |     指定可用于启动操作系统早于 Windows Vista 操作系统加载器 (Ntldr)。|
|    {fwbootmgr}        |     指定特定于实现可扩展固件接口 (EFI) 规范的系统固件启动管理器入口。|

## <a name="boot-option-inheritance"></a>启动选项继承

可以继承某些启动设置。 这样的设置组就可以在不同的引导方案中，例如当从休眠恢复时使用。

使用 bcdedit 命令 /enum 选项可显示有关的任何标识符的信息。

在下面的示例中，{当前} 的标识符上显示的信息显示它继承 {bootloadersettings}

```console
C:\>bcdedit /enum {current}

Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.exe
description             Windows 10
locale                  en-US
inherit                 {bootloadersettings}
...
```

使用 bcdedit /enum 命令以查看哪些设置会继承。

在以下示例中，{globalsettings}，继承 {dbgsettings} 中设置的任何 {emssettings} 和 {badmemory}。

```console
C:\>bcdedit /enum {globalsettings}

Global Settings
---------------
identifier              {globalsettings}
inherit                 {dbgsettings}
                        {emssettings}
                        {badmemory}
```

使用与 bcdedit /enum 继承选项显示有关继承的信息。

在下面的示例中，{bootloadersettings} 继承 {globalsettings} 和 {hypervisorsettings} 和 {resumeloadersettings} 继承 {globalsettings}。

```console
C:\>bcdedit /enum inherit

...

Boot Loader Settings
--------------------
identifier              {bootloadersettings}
inherit                 {globalsettings}
                        {hypervisorsettings}


Resume Loader Settings
----------------------
identifier              {resumeloadersettings}
inherit                 {globalsettings}

...

```

使用 bcdedit/所有命令以查看所有设置。  

```console
C:\>bcdedit /enum all

Windows Boot Manager
--------------------
identifier              {bootmgr}
device                  partition=\Device\HarddiskVolume1
description             Windows Boot Manager

...

```

## <a name="guids-and-identifiers"></a>Guid 和标识符

标识符使用全局唯一标识符或 GUID。 GUID 具有以下格式，其中每个"x"表示十六进制数字。 由于使用 Guid 是容易出错，因此建议使用英语的标识符名称，例如 {current} 若要使用当前配置的 Windows 的启动信息。

```guid
{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}
```

例如：

```guid
{d2b69192-8f14-11da-a31f-ea816ab185e9}
```
短划线 （-） 和的开头和结尾的 guid 在大括号的位置是必需的。

使用 bcdedit /enum /v 来显示与标识符相关联的 Guid。

```console
C:\>bcdedit /enum /v

Windows Boot Manager
--------------------
identifier              {9dea862c-5cdd-4e70-acc1-f32b344d4795}
device                  partition=\Device\HarddiskVolume1
description             Windows Boot Manager
locale                  en-US
inherit                 {7ea2e1ac-2e61-4728-aaa3-896d9d0a9f0e}
```
