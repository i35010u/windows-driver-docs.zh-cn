---
title: 将设备标记为具有要执行的 Finish-Install 操作
description: 将设备标记为具有要执行的 Finish-Install 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a972cbb69163e8370540681beb9689248409ecd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816665"
---
# <a name="marking-a-device-as-having-a-finish-install-action-to-perform"></a>将设备标记为具有要执行的 Finish-Install 操作


*安装* 程序 (类安装程序、类共同安装程序或设备共同安装程序) 向 Windows 表明，在安装程序处理 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md)请求时，通过设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志来完成安装操作。 此操作会导致 Windows 将设备标记为需要执行 "完成安装" 操作。 步骤如下：

1.  当安装程序收到 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求时，如果安装程序已完成安装操作，则安装程序将设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志。

    然后，安装程序将返回以下错误代码之一：

    -   ERROR_DI_DO_DEFAULT 如果安装程序是一个没有完成安装向导页的类安装程序。
    -   NO_ERROR 如果安装程序是具有完成安装向导页面的类安装程序，或者具有或没有 "完成安装向导" 页面的共同安装程序。

2.  如果在所有安装程序都已处理设备的 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求之后为设备设置了 DI_FLAGSEX_FINISHINSTALL_ACTION 标志，则 Windows 将标记设备，以执行 "完成安装" 操作。

 

