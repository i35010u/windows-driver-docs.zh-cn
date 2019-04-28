---
title: 否认
description: 否认
ms.assetid: ccb50b6c-9e7d-4a90-a049-6c62b1b57376
keywords:
- 威胁建模 WDK 的文件系统，否认性
- 安全威胁模型 WDK 的文件系统，否认性
- 不可否认 WDK 的文件系统
- 所有权 WDK 的文件系统
- 拒绝执行操作 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bfcea232582eb22b2e158eef38bb085df1994b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344573"
---
# <a name="repudiation"></a>否认


## <span id="ddk_repudiation_if"></span><span id="DDK_REPUDIATION_IF"></span>


不可否认的概念是用户可能会执行特定操作，并随后否认执行它。 对于大多数驱动程序，这是问题的异常类型。 对于文件系统，但是，日志记录用于跟踪操作 （删除了重要的文件，例如），并确保操作的明确记录。 这提供了一种机制来确保对此类否认性。

此外，操作系统可将对象的所有权分配给特定的安全标识符。 不适当的特权，无法更改所有权信息 (**SeTakeOwnershipPrivilege**) 以确保可以跟踪的特定对象的所有权。 对象所有权提供了另一种形式的保护措施否认性。

 

 




