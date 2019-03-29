---
title: 管理多个附加的提供程序模块
description: 管理多个附加的提供程序模块
ms.assetid: 307cfbf8-e5a3-4c01-abf5-5b2eea250d77
keywords:
- 提供程序 WDK 网络模块注册机构，附加多个模块
- 客户端模块 WDK 网络模块注册机构，多个附加
- WDK 网络模块注册机构的多个附加的网络模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb75baf40f971a90067f58a770793490d840c52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565972"
---
# <a name="managing-multiple-attached-provider-modules"></a>管理多个附加的提供程序模块


单个客户端模块可以附加到多个提供程序的模块。 若要管理附加提供程序的多个模块，绑定句柄、 提供程序模块的绑定上下文和附加到每个提供程序模块提供程序模块的调度表，必须单独保存客户端模块。 通常将此数据保存在客户端模块的绑定上下文中为每个附件。 但是，客户端模块可以管理它选择的任何方式在每个附加提供程序模块的数据。

一个[网络编程接口 (NPI)](network-programming-interface.md)通常定义的客户端模块回调函数，以便它们包括到客户端模块的绑定上下文的指针，或者作为之一的某个其他特定于 NPI 的标识符函数参数。 因此，客户端模块可以确定哪个提供程序模块时，调用方调用其中一个 NPI 回调函数。

 

 





