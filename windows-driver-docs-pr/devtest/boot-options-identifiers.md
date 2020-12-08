---
title: 启动选项标识符
description: 描述启动选项标识符
keywords:
- 启动选项窗口
- 标识符
- default
- WDK 启动选项
ms.date: 04/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: bbe2567272e36b3a69f0d656b302538571f02e41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801871"
---
# <a name="boot-options-identifiers"></a>启动选项标识符

许多 bcdedit 命令都需要标识符。 标识符用于唯一标识启动设置存储中包含的项。 

使用 bcdedit/enum 显示标识符。

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

可以通过众所周知的标识符标识多个条目。 如果某个条目具有已知标识符，则除非使用了/v 命令行开关，否则 bcdedit 会将其显示在输出中。 有关详细信息，请运行 "bcdedit/？ /v "。

通常使用常见的众所周知标识符：

| 标识符           | 说明
|-----------------------|----------------------------------------------------------------------|
|    缺省值          |     指定与启动管理器默认应用程序项相对应的虚拟标识符。 | 
|    当前          |     指定对应于当前正在运行的操作系统的操作系统启动应用程序项的虚拟标识符。 |
|    bootmgr          |     指定 Windows 启动管理器应用程序条目。 |

任何启动应用程序条目都可以继承这些常见的常见标识符：

| 标识符           | 说明
|-----------------------|----------------------------------------------------------------------|
|    globalsettings    |    包含应由所有启动应用程序项继承的全局设置的集合。 |
|   {bootloadersettings} |   包含应由所有启动加载器应用程序项继承的全局设置的集合。 |

还可以使用这些众所周知的标识符：

| 标识符           | 说明
|-----------------------|----------------------------------------------------------------------|
|    dbgsettings       |    包含可以由任何启动应用程序项继承的全局调试器设置。 |
|    {hypervisorsettings} |   包含可由任何 OS 加载器项继承的虚拟机监控程序设置。 |
|    emssettings       |  包含可以由任何启动应用程序项继承的全局紧急管理服务设置。 |
|    {resumeloadersettings} | 包含全局设置的集合，这些设置应由所有 Windows 从休眠状态恢复应用程序项继承。 |
|    {badmemory}         |    包含可以由任何启动应用程序项继承的全局 RAM 缺陷列表。 |
|   memdiag           |    指定内存诊断应用程序条目。 |
|    {ramdiskoptions}    |   包含用于 RAM 磁盘设备的启动管理器所需的其他选项。 |

这些众所周知的标识符与早期版本的 Windows 一起使用：

| 标识符           | 说明
|-----------------------|----------------------------------------------------------------------|
|    ntldr            |     指定 OS 加载器 (Ntldr) ，可用于启动 Windows Vista 之前的操作系统。|
|    {fwbootmgr}        |     指定固件启动管理器条目，具体取决于实现 (EFI) 规范的可扩展固件接口的系统。|

## <a name="boot-option-inheritance"></a>启动选项继承

某些启动设置可以继承。 这允许在不同的启动方案中使用设置组，例如在从休眠状态恢复时。

使用 bcdedit command/enum 选项可以显示有关任何标识符的信息。

在下面的示例中，显示 {current} 标识符的信息显示它继承了 {bootloadersettings}

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

使用 bcdedit/enum 命令可查看要继承哪些设置。

在下面的示例中，{globalsettings} 继承了 {dbgsettings}、{emssettings} 和 {badmemory} 中设置的任何内容。

```console
C:\>bcdedit /enum {globalsettings}

Global Settings
---------------
identifier              {globalsettings}
inherit                 {dbgsettings}
                        {emssettings}
                        {badmemory}
```

使用带有 bcdedit/enum 的 inherit 选项可以显示有关继承的信息。

在下面的示例中，{bootloadersettings} 继承了 {globalsettings}，{hypervisorsettings} 和 {resumeloadersettings} 继承了 {globalsettings}。

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

使用 bcdedit/all 命令查看所有设置。  

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

标识符使用全局唯一标识符或 GUID。 GUID 具有以下格式，其中每个 "x" 表示一个十六进制数字。 由于使用 Guid 容易出错，因此建议使用英语标识符名称（如 {current}）来处理为 Windows 配置的当前启动信息。

```guid
{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}
```

例如：

```guid
{d2b69192-8f14-11da-a31f-ea816ab185e9}
```
需要为短划线 (-) 的位置以及 GUID 开头和结尾处的大括号。

使用 bcdedit/enum/v 显示与标识符关联的 Guid。

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
