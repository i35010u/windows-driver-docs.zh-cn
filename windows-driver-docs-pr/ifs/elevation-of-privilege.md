---
title: 特权提升
description: 特权提升
ms.assetid: 08e20c51-fbc1-4e38-b12d-f123e4a2ba10
keywords:
- 威胁建模 WDK 文件系统中，提升权限
- 安全威胁模型 WDK 文件系统中，提升权限
- 特权提升 WDK 的文件系统
- 缓冲区 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4eddd123c4b2db1d7ef04d841dced68ed813d82
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383853"
---
# <a name="elevation-of-privilege"></a>特权提升


## <span id="ddk_elevation_of_privilege_if"></span><span id="DDK_ELEVATION_OF_PRIVILEGE_IF"></span>


当应用程序获得权限或不应提供给他们的权限时，会发生特权提升。 许多特权提升攻击都类似于其他威胁的攻击。 例如，缓冲区溢出攻击巧妙地试图写入可执行代码。 这适用于基于 x86 的体系结构时从堆栈上为局部变量分配缓冲区。 堆栈还包含在当前过程调用的返回地址。 如果恶意开发人员查明存在潜在的缓冲区溢出，数据可以放入了缓冲区中，以便它将覆盖到的回邮地址。 CPU 执行时返回到上一个调用方的"ret"指令，它会将控制权返还给恶意开发人员并不是实际调用方指定的位置。

对于文件系统和文件系统筛选器驱动程序，可能会提升-特权的攻击是非常高，因为以下原因的组合：

-   文件系统和文件系统筛选器驱动程序将积极参与管理对数据，包括权限的访问。

-   文件系统和文件系统筛选器驱动程序利用特殊权限和访问权限来实现其功能。

-   许多操作系统权限直接与文件系统 (**SeChangeNotifyPrivilege**，它可以控制能够遍历目录，例如)。

这种类型是攻击的最重要的实现文件系统。 这种攻击可以是文件系统筛选器驱动程序的积极地管理数据存储 （例如，加密筛选器） 可能会绕过或绕过普通的文件系统安全操作问题。

 

 




