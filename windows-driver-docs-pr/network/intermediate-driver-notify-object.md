---
title: 中间驱动程序通知对象
description: 中间驱动程序通知对象
ms.assetid: 756e02ff-5e30-4511-af4c-b7be9830898c
keywords:
- 通知对象 WDK 网络连接、 中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bdc7bc871446b4a8308949c4376a7da33bd3be8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391658"
---
# <a name="intermediate-driver-notify-object"></a>中间驱动程序通知对象





*中间驱动程序通知对象*是网络类安装程序的扩展。 网络类安装程序将加载和初始化通知对象并将其发送通知的事件 （如虚拟微型端口删除通知） 与您的驱动程序相关。 如果您在一般情况下想要通知的对象的概述或有关的信息通知对象，请参阅[通知网络组件的对象](notify-objects-for-network-components.md)。

若要在安装中包括的通知对象，必须在中间驱动程序协议 INF 中引用它。 筛选器中间驱动程序不需要通知对象。 如果你想要向用户提供更灵活的配置选项，可以使用筛选器中间驱动程序包含通知对象。

在 Windows Vista 中，可以使用通知对象或自定义安装应用程序微型端口 INF 文件复制到系统 INF 目录。 对于任何一种方法，你使用**SetupCopyOEMInf** （Microsoft Windows SDK 文档中所述） 来复制 INF。 对于 Windows Vista 及更高版本的操作系统版本，应使用[ **INF CopyINF 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547317)协议 INF 复制微型端口 INF 中。 有关复制 INF 文件的详细信息，请参阅[复制 Inf](https://msdn.microsoft.com/library/windows/hardware/ff540117)。

MUX 中间驱动程序通知对象必须提供服务来安装和删除虚拟微型端口。 这可以自动或通过提供用户界面。 它必须管理在注册表中的虚拟微型端口的设备名称列表。 设备名称列表定义虚拟微型端口与物理设备之间的绑定。 例如，n 对一 MUX 中间驱动程序示例通知对象维护虚拟微型端口绑定到每个物理设备的列表**UpperBindings**注册表项。 MUX 示例驱动程序读取**UpperBindings**列表并初始化每个条目虚拟微型端口。

MUX 中间驱动程序应使用**UpperRange**/**LowerRange**条目来控制外部绑定。 但是，您可以控制外部绑定从通知对象，如有必要。 有关中间驱动程序中的绑定的详细信息，请参阅[中间驱动程序 UpperRange 和 LowerRange INF 文件条目](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)

通知对象可以选择提供一个用户界面，允许用户更改或查看您的驱动程序的配置。 MUX 中间驱动程序示例包括通知对象的示例用户界面。

 

 





