---
title: 使驱动程序代码或数据可分页
description: 使驱动程序代码或数据可分页
ms.assetid: c4ffd222-8ea5-48df-9c79-7d68e5462b3e
keywords:
- 内存管理 WDK 内核，可分页的驱动程序
- 可分页的驱动程序 WDK 内核设置
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f03445b66b962193a64deb4e7522c884f05ea2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569306"
---
# <a name="making-driver-code-or-data-pageable"></a>使驱动程序代码或数据可分页





若要使驱动程序例程可分页，您必须确保它运行在 IRQL&lt;调度\_级别和，它并不获取任何旋转锁。

本部分包含以下主题：

[可以是可分页的检测代码](detecting-code-that-can-be-pageable.md)

[隔离可分页的代码](isolating-pageable-code.md)

[锁定的可分页代码或数据](locking-pageable-code-or-data.md)

[分页整个驱动程序](paging-an-entire-driver.md)

 

 




