---
title: 管理多个附加的客户端模块
description: 管理多个附加的客户端模块
keywords:
- 提供商模块 WDK 网络模块注册器，多个附加
- 客户端模块，WDK 网络模块注册器，多个附加
- 多个连接的网络模块 WDK 网络模块注册器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6670ffc90d35ff4cdfc7ad51593e618609bbce5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794454"
---
# <a name="managing-multiple-attached-client-modules"></a>管理多个附加的客户端模块


单个提供程序模块可以附加到多个客户端模块。 若要管理多个附加的客户端模块，提供程序模块必须为它附加到的每个客户端模块独立保存绑定句柄、客户端模块的绑定上下文和客户端模块的调度表。 通常，此数据保存在提供程序模块的每个附件的绑定上下文中。 但是，提供程序模块可以以任何所选的方式管理每个附加客户端模块的数据。

[ (NPI) 的网络编程接口](network-programming-interface.md)通常定义提供程序模块函数，以使其包含指向提供程序模块的绑定上下文的指针或其他一些特定于 NPI 的标识符作为函数参数之一。 因此，当调用某个客户端模块的 NPI 函数时，该模块可以确定哪个客户端模块为调用方。

 

 





