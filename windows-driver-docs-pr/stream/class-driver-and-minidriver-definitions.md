---
title: 类驱动程序和微型驱动程序定义
description: 类驱动程序和微型驱动程序定义
ms.assetid: eb428e8b-0c47-4843-8770-c22088ba5c6c
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，类驱动程序/微型驱动程序关系
- 流式处理微型驱动程序 WDK Windows 2000 内核，类驱动程序/微型驱动程序关系
- 微型驱动程序 WDK Windows 2000 内核流式处理、 类驱动程序/微型驱动程序关系
- 类驱动程序/微型驱动程序关系 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53064efc1c1e1fa27df7b0b96bbc72ed07fbff4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565087"
---
# <a name="class-driver-and-minidriver-definitions"></a>类驱动程序和微型驱动程序定义





Microsoft 提供的类驱动程序是旨在提供一个简单的界面，供应商编写的微型驱动程序和操作系统之间的中间驱动程序。 微型驱动程序是使用 Microsoft 提供的类驱动程序以完成执行函数调用的大多数操作，并提供仅特定于设备的控件的特定于硬件的 DLL。

下 WDM，微型驱动程序注册类驱动程序，其相关联的硬件适配器并在类驱动程序创建文件对象来表示每个注册的适配器。 微型驱动程序使用的类驱动程序的设备对象发出系统调用。 通过使用 WDM 流式处理的用户模式下客户端访问的类驱动程序。

类驱动程序和微型驱动程序之间的交互包括：

-   微型驱动程序不会创建一个设备对象，但它们共享根据需要在类驱动程序的设备对象。 这可节省系统资源。

-   每个适配器创建只有一个设备对象。 多个子设备 (称为*流*) 适配器支持的流式处理 WDM 插针表示。

 

 




