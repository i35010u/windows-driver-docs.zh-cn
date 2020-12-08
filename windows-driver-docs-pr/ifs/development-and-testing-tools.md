---
title: 开发和测试工具
description: 开发和测试工具
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，工具
- Fltmc.exe WDK 文件系统微筛选器
- fltkd 调试器扩展 WDK 文件系统微筛选器
- 筛选器验证程序 WDK 文件系统微筛选器
- 验证程序实用工具
ms.date: 08/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4c833945152ebd89de3fc4b7c82c52cfed4330c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823259"
---
# <a name="development-and-testing-tools"></a>开发和测试工具

可以使用多个筛选器管理器工具。 还鼓励微筛选器驱动程序开发人员使用一般用途的内核模式开发和测试工具，如使用驱动程序特定的规则 PREfast。

## <a name="fltmcexe-command"></a>Fltmc.exe 命令

*Fltmc.exe* 程序是系统提供的用于常见微筛选器驱动程序管理操作的命令行实用程序。 开发人员可以使用 *Fltmc.exe* 来加载和卸载微筛选器驱动程序、附加或分离微筛选器驱动程序和枚举微筛选器驱动程序、实例和卷。 在具有管理员权限的命令提示符下，键入 ```fltmc help``` 以查看完整的命令列表。

## <a name="fsutilexe-command"></a>Fsutil.exe 命令

[*Fsutil.exe*](/windows-server/administration/windows-commands/fsutil-file)程序是系统提供的命令行实用程序，用于对文件执行各种操作。 开发人员可以键入， ```fsutil file layout foo.md``` 以美观的方式打印文件的所有详细信息，如属性、时间戳、流等。

## <a name="fltkd-debugger-extension"></a>！ fltkd 调试器扩展

[Windows 调试](../debugger/index.md)工具中提供了！ fltkd 调试器扩展。 常用命令包括以下内容：

| 命令 | 描述 |
| ------- | ----------- |
| **!cbd** | 筛选器管理器等效于！ irp |
| **！筛选器** | 列出有关指定筛选器的详细信息 |
| **！筛选器** | 列出所有附加的微筛选器驱动程序 |
| **！帧** | 列出所有筛选器管理器框架和附加的微筛选器驱动程序 |
| **！实例** | 列出有关指定实例的详细信息 |
| **！卷** | 列出有关指定卷的详细信息 |
| **！卷** | 列出所有卷和连接的微筛选器驱动程序实例 |

在 WinDbg 中，键入 **！ fltkd** 作为完整命令列表的帮助。

## <a name="filter-verifier"></a>筛选器验证程序

筛选器验证[程序是驱动程序验证](../devtest/driver-verifier.md)器中的一个[i/o 验证](../devtest/i-o-verification.md)选项，用于验证筛选器管理器功能的微筛选器驱动程序使用情况。 筛选器验证程序与筛选器管理器一起安装。 开发人员应始终启用驱动程序验证程序和筛选器验证程序，开发微筛选器驱动程序。

要使用筛选器验证程序，请在驱动程序验证程序中指定微筛选器驱动程序的名称并启用 i/o 验证选项 (*Verifier.exe*) 。 当微筛选器驱动程序向筛选器管理器注册时，将开始验证。

筛选器验证器在微筛选器驱动程序中验证以下用法：

* 正确使用参数和调用上下文
* Preoperation 和 postoperation 回调例程的正确返回值
* 回调数据中参数的一致和连贯更改

筛选器验证器跟踪以下筛选器管理器对象：

* 上下文
* 回调数据结构
* 已排队的工作项
* NameInformation 结构
* 文件对象
* 筛选对象
* 实例对象
* 卷对象

在命令提示符下，键入 ```verifier /?``` 以查看语法和参数的完整列表。
