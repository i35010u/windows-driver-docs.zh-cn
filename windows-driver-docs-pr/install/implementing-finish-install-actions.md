---
title: 实施 Finish-Install 操作
description: 实施 Finish-Install 操作
ms.assetid: accdf2f5-f324-41dc-afc1-18e03b422fcc
keywords:
- 完成安装操作 WDK 设备安装
- WDK 完成安装操作
- DI_FLAGSEX_FINISHINSTALL_ACTION
- DIF_FINISHINSTALL_ACTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 864dc05160af9936e933627232d0be9302498b43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373194"
---
# <a name="implementing-finish-install-actions"></a>实施 Finish-Install 操作


*安装程序*（安装程序类、 类共同安装程序中或设备共同安装程序） 提供完成安装操作。 完成安装操作可以运行可执行程序、 创建过程，创建一个线程，或在设备驱动程序安装完成安装过程中执行代码。

若要执行的操作完成安装，安装程序：

1.  安装程序在处理时设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702) DIF 代码，并返回以下错误代码之一：
    -   如果它是类安装程序而无需完成安装向导页，ERROR_DI_DO_DEFAULT。
    -   如果它是使用完成安装向导页或带或不带完成安装向导页的共同安装程序类安装程序，NO_ERROR。

2.  执行完成安装操作，在处理时会[ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)请求。

    安装程序将返回一个错误代码如下表中。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">错误代码</th>
    <th align="left">含义</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>ERROR_DI_DO_DEFAULT</p></td>
    <td align="left"><p>安装程序类：类安装程序成功运行其完成安装操作，并正在请求 Windows 来执行其默认处理。 类安装程序还应返回此错误代码，如果它具有未完成安装操作。</p>
    <p>设备或类共同安装程序：共同安装程序不会返回此错误代码。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>NO_ERROR</p></td>
    <td align="left"><p>安装程序类：类安装程序已成功运行其完成安装操作。 Windows 不应执行默认处理。</p>
    <p>设备或类共同安装程序：辅助安装程序已成功运行其完成安装操作，或者具有未完成安装操作。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Microsoft Win32 错误</p></td>
    <td align="left"><p>安装程序遇到错误，但完成安装操作应该重试。 返回一个 Win32 错误代码指示 Windows 应运行另一个完成安装过程完成下一次枚举设备的完成安装操作。</p></td>
    </tr>
    </tbody>
    </table>




**请注意**如果完成安装操作失败，并且不应再次尝试、 类安装程序将返回 ERROR_DI_DO_DEFAULT 和设备或类共同安装程序将返回 NO_ERROR。




有关如何开发完成安装操作的信息，请参阅[实现完成安装操作指南](guidelines-for-implementing-finish-install-actions.md)演示如何实现完成安装操作的示例代码，请参阅以下主题：

[代码示例：在类安装程序完成安装操作](code-example--finish-install-actions-in-a-class-installer.md)

[代码示例：在共同安装程序完成安装操作](code-example--finish-install-actions-in-a-co-installer.md)









