---
title: 管理多个连接的客户端模块
description: 管理多个连接的客户端模块
ms.assetid: dcb2ebba-6df7-47d5-97b6-ed2691b5e6c8
keywords:
- 提供程序 WDK 网络模块注册机构，附加多个模块
- 客户端模块 WDK 网络模块注册机构，多个附加
- WDK 网络模块注册机构的多个附加的网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f36f764e8dceef2c3081dbff4c53196a60bf9531
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555396"
---
# <a name="managing-multiple-attached-client-modules"></a>管理多个连接的客户端模块


单个提供程序模块可以附加到多个客户端模块。 若要管理多个连接的客户端模块，提供程序模块必须单独保存绑定句柄、 客户端模块的绑定上下文和附加到每个客户端模块的客户端模块的调度表。 此数据通常保存为每个附件的提供程序模块的绑定上下文中。 但是，提供程序模块可以管理它选择的任何方式在每个连接的客户端模块的数据。

一个[网络编程接口 (NPI)](network-programming-interface.md) ，使其作为一个函数包含指向提供程序模块的绑定上下文的指针，或者某些其他特定于 NPI 的标识符通常定义提供程序模块函数参数。 因此，提供程序模块可以确定哪些客户端模块，是调用方调用 NPI 函数之一时。

 

 





