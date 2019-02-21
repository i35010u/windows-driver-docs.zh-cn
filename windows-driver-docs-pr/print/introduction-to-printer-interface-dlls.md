---
title: 打印机接口 dll 函数简介
description: 打印机接口 dll 函数简介
ms.assetid: 1993d818-9761-418e-96c3-e3c46965bef1
keywords:
- 打印机接口 DLL WDK 有关打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d6f65a96b58a4557f128d52727c6e70ace6149c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521865"
---
# <a name="introduction-to-printer-interface-dlls"></a>打印机接口 dll 函数简介





打印机通常向用户提供大量可更改每个文档打印时的可修改的配置选项。 选项，例如白皮书、 任务栏和字体选择，以及图像分辨率、 大小、 颜色和等等，必须可通过用户界面可以由应用程序调用。

打印机驱动程序*打印机接口 DLL*，它将执行在用户模式下，负责将用户界面导出到打印机的配置选项。 提供此接口涉及[创建的打印机的属性表页](creating-property-sheet-pages-for-printers.md)。 应用程序 （例如打印的文件夹中） 通过调用 Win32 函数导出由打印后台处理程序，显示的界面和后台处理程序，反过来，调用[定义由打印机接口 Dll 函数](functions-defined-by-printer-interface-dlls.md)。

提供配置选项的用户界面不是打印机接口 DLL 的唯一职责。 此外将 DLL 导出函数的后台处理程序可以调用以通知与打印相关的系统事件，如驱动程序安装和升级，或打印机新增功能和连接的驱动程序。

 

 




