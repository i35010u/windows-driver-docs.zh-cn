---
title: 管理多个附加的提供程序模块
description: 管理多个附加的提供程序模块
keywords:
- 提供商模块 WDK 网络模块注册器，多个附加
- 客户端模块，WDK 网络模块注册器，多个附加
- 多个连接的网络模块 WDK 网络模块注册器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cc481b9040f91cf40f7f8ca2b8ab5152bf2dbde
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794487"
---
# <a name="managing-multiple-attached-provider-modules"></a>管理多个附加的提供程序模块


单个客户端模块可以附加到多个提供程序模块。 若要管理多个附加的提供程序模块，客户端模块必须独立保存绑定句柄、提供程序模块的绑定上下文，以及它所附加到的每个提供程序模块的提供程序模块的调度表。 通常，此数据保存在每个附件的客户端模块的绑定上下文中。 但是，客户端模块可以以任何所选的方式管理每个附加提供程序模块的数据。

[ (NPI) 的网络编程接口](network-programming-interface.md)通常定义了客户端模块回调函数，使其包含指向客户端模块的绑定上下文的指针或其他一些特定于 NPI 的标识符作为函数参数之一。 因此，当调用其中一个 NPI 回调函数时，客户端模块可以确定哪个提供程序模块是调用方。

 

 





