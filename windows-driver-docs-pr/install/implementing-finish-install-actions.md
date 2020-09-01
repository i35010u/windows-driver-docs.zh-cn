---
title: 实施 Finish-Install 操作
description: 实施 Finish-Install 操作
ms.assetid: accdf2f5-f324-41dc-afc1-18e03b422fcc
keywords:
- 完成-安装操作 WDK 设备安装
- 操作 WDK 完成-安装
- DI_FLAGSEX_FINISHINSTALL_ACTION
- DIF_FINISHINSTALL_ACTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6e22a74db4668c7e278c91e56fa828eb5afb65b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097103"
---
# <a name="implementing-finish-install-actions"></a>实施 Finish-Install 操作


*安装* 程序 (类安装程序、类共同安装程序或设备共同安装程序) 提供完成安装操作。 "完成-安装" 操作可以运行可执行程序、创建进程、创建线程或执行设备驱动程序安装完成-安装过程中的代码。

若要实现安装后操作，请执行以下操作：

1.  当安装程序处理 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 的 DIF 代码并返回以下错误代码之一时，设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志：
    -   如果是没有完成安装向导页面的类安装程序，则 ERROR_DI_DO_DEFAULT。
    -   NO_ERROR 如果是具有完成安装向导页面的类安装程序，或具有或不包含完成安装向导页面的共同安装程序。

2.  当处理 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求时，执行完成安装操作。

    安装程序返回下表中的错误代码之一。

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
    <td align="left"><p>类安装程序：类安装程序已成功运行其完成安装操作，并请求 Windows 执行其默认处理。 如果类安装程序没有完成安装操作，还应返回此错误代码。</p>
    <p>设备或类共同安装程序：共同安装程序不会返回此错误代码。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>NO_ERROR</p></td>
    <td align="left"><p>类安装程序：类安装程序已成功运行其完成安装操作。 Windows 不应执行其默认处理。</p>
    <p>设备或类共同安装程序：共同安装程序已成功运行其完成安装操作或没有完成安装操作。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Microsoft Win32 错误</p></td>
    <td align="left"><p>安装程序遇到错误，但应再次尝试 "完成-安装" 操作。 返回一个 Win32 错误代码表示 Windows 应运行另一个完成安装过程，以便在下次枚举设备时完成完成安装操作。</p></td>
    </tr>
    </tbody>
    </table>




**注意**   如果完成安装操作失败且不应重试，则类安装程序将返回 ERROR_DI_DO_DEFAULT 并且设备或类共同安装程序将返回 NO_ERROR。




有关如何开发 "完成-安装" 操作的信息，请参阅为演示如何实现完成-安装操作的示例代码 [实现完成安装操作的准则](guidelines-for-implementing-finish-install-actions.md) ，请参阅以下主题：

[代码示例：类安装程序中的 Finish-Install 操作](code-example--finish-install-actions-in-a-class-installer.md)

[代码示例：辅助安装程序中的 Finish-Install 操作](code-example--finish-install-actions-in-a-co-installer.md)