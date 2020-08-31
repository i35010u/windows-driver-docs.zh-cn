---
title: 将设备标记为具有完成安装操作才能执行
description: 将设备标记为具有完成安装操作才能执行
ms.assetid: 7f2560e6-94a7-4dd0-aa2a-e6cdd96c6d9b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8dcb621adf2a0efbd63e399c5bacbd251347195
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095863"
---
# <a name="marking-a-device-as-having-a-finish-install-action-to-perform"></a>将设备标记为具有完成安装操作才能执行


*安装*程序 (类安装程序、类共同安装程序或设备共同安装程序) 向 Windows 表明，在安装程序处理[**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md)请求时，通过设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志来完成安装操作。 此操作会导致 Windows 将设备标记为需要执行 "完成安装" 操作。 步骤如下：

1.  当安装程序收到 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求时，如果安装程序已完成安装操作，则安装程序将设置 DI_FLAGSEX_FINISHINSTALL_ACTION 标志。

    然后，安装程序将返回以下错误代码之一：

    -   ERROR_DI_DO_DEFAULT 如果安装程序是一个没有完成安装向导页的类安装程序。
    -   NO_ERROR 如果安装程序是具有完成安装向导页面的类安装程序，或者具有或没有 "完成安装向导" 页面的共同安装程序。

2.  如果在所有安装程序都已处理设备的 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) 请求之后为设备设置了 DI_FLAGSEX_FINISHINSTALL_ACTION 标志，则 Windows 将标记设备，以执行 "完成安装" 操作。

 

