---
title: 何时使用内核模式 KTM
description: 何时使用内核模式 KTM
ms.assetid: deb3372d-19c4-4a17-b499-1da485e89276
keywords:
- 内核事务管理器 WDK 何时使用
- KTM WDK 何时使用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a04e09626fd8034e7738ba9274af7ee7f905f510
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366749"
---
# <a name="when-to-use-kernel-mode-ktm"></a>何时使用内核模式 KTM


可以使用内核模式 KTM 与内核模式组件，以在内核模式下支持事务处理的操作或协调使用内核模式 KTM 的内核模式组件和使用用户模式下 KTM 的用户模式组件之间的事务处理的操作。

例如，您可以在以下情况下使用 KTM:

-   内核模式驱动程序必须打开文件、 修改文件的内容，并保存修改的文件，并且它必须到该文件防止破坏，如果写入操作失败。 如果您的驱动程序执行这些操作在事务中的，该驱动程序没有为复制和旧文件重命名、 修改新副本，、 删除旧的文件，然后重命名新副本。

-   设计一个新的数据存储系统，将信息存储在一个或多个数据库中。 您的系统的组件将访问在内核模式下，或可能是在用户模式和内核模式下的数据库。 系统的事务性客户端将封装在事务内的其数据库操作，以便对所有数据库的所有修改成功或失败作为一个单元。

 

 




