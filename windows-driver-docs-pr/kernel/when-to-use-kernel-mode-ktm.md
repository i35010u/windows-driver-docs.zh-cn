---
title: 何时使用内核模式 KTM
description: 何时使用内核模式 KTM
keywords:
- 内核事务管理器 WDK，何时使用
- KTM WDK，何时使用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13d80be70a5495d80b0350717fdbc7050780c29c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832277"
---
# <a name="when-to-use-kernel-mode-ktm"></a>何时使用内核模式 KTM


你可以对内核模式组件使用内核模式 KTM，以支持内核模式下的事务处理操作，或者协调使用内核模式 KTM 的内核模式组件和使用用户模式 KTM 的用户模式组件之间的事务处理操作。

例如，你可能会在以下情况下使用 KTM：

-   内核模式驱动程序必须打开文件、修改文件内容并保存修改后的文件，如果写入操作失败，则必须防止文件损坏。 如果你的驱动程序在事务中执行这些操作，则驱动程序不必复制和重命名旧文件、修改新副本、删除旧文件，然后重命名新副本。

-   正在设计将信息存储在一个或多个数据库中的新数据存储系统。 系统的组件将以内核模式或同时在用户模式和内核模式下访问数据库。 系统的事务客户端会将其数据库操作封装在事务中，以便对所有数据库的所有修改要么作为一个单元成功或失败。

 

 




