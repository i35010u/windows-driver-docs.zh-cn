---
title: 类驱动程序和微型驱动程序定义
description: 类驱动程序和微型驱动程序定义
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核、类驱动程序/微型驱动程序关系
- 流式处理微型驱动程序 WDK Windows 2000 内核、类驱动程序/微型驱动程序关系
- 微型驱动程序 WDK Windows 2000 内核流式处理，类驱动程序/微型驱动程序关系
- 类驱动程序/微型驱动程序关系 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28dfafd489646c9dc4c14ccb3403221d9840a845
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788189"
---
# <a name="class-driver-and-minidriver-definitions"></a>类驱动程序和微型驱动程序定义





Microsoft 提供的类驱动程序是一个中间驱动程序，旨在提供供应商编写的微型驱动程序和操作系统之间的简单接口。 微型驱动程序是特定于硬件的 DLL，它使用 Microsoft 提供的类驱动程序通过函数调用来完成大多数操作，只提供特定于设备的控件。

在 WDM 下，微型驱动程序将其关联的硬件适配器注册到类驱动程序，类驱动程序将创建一个文件对象来表示注册的每个适配器。 微型驱动程序使用类驱动程序的设备对象进行系统调用。 类驱动程序通过 WDM 流式处理由用户模式客户端访问。

类驱动程序和微型驱动程序之间的交互包括：

-   微型驱动程序不会创建设备对象，但会根据需要共享类驱动程序的设备对象。 这将保存系统资源。

-   每个适配器只创建一个设备对象。 适配器支持的多个 subdevices (称为 *流*) 由 WDM 流 pin 表示。

 

 




