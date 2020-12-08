---
title: 权限提升
description: 权限提升
keywords:
- 威胁模型 WDK 文件系统，特权提升
- 安全威胁模型 WDK 文件系统，特权提升
- 特权提升 WDK 文件系统
- 缓冲 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c471c0c58de70cdead99ff71ecbe5d579b275c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806307"
---
# <a name="elevation-of-privilege"></a>权限提升


## <span id="ddk_elevation_of_privilege_if"></span><span id="DDK_ELEVATION_OF_PRIVILEGE_IF"></span>


当应用程序获得了不可用于它们的权限或特权时，会发生特权提升。 许多特权提升攻击类似于其他威胁的攻击。 例如，巧妙尝试写入可执行代码的缓冲区溢出攻击。 这适用于基于 x86 的体系结构，当缓冲区作为本地变量从堆栈中分配时。 堆栈还包含当前过程调用的返回地址。 如果恶意开发人员 ascertains 存在缓冲区溢出的可能性，则可以将数据放入缓冲区，使其覆盖返回地址。 当 CPU 执行 "ret" 指令以返回到上一个调用方时，它会将控制权返回给恶意开发人员指定的位置，而不是实际调用方。

对于文件系统和文件系统筛选器驱动程序，由于以下原因组合，导致特权提升攻击的可能性很高：

-   文件系统和文件系统筛选器驱动程序积极涉及管理对数据的访问，包括特权。

-   文件系统和文件系统筛选器驱动程序利用特殊权限和访问权限来实现其功能。

-   许多操作系统特权直接与文件系统 (**SeChangeNotifyPrivilege**，后者控制遍历目录的能力，例如) 。

这种类型的攻击对于实现文件系统最为重要。 这种攻击可能会对文件系统筛选器驱动程序（主动管理数据存储 (加密筛选器）出现问题，例如) 可能会绕过或绕过正常文件系统安全操作。

 

 




