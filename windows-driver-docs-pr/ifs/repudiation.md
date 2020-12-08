---
title: 否认
description: 否认
keywords:
- 威胁模型 WDK 文件系统，抵赖
- 安全威胁模型 WDK 文件系统，抵赖
- 抵赖 WDK 文件系统
- 所有权 WDK 文件系统
- 拒绝执行操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70461d2660f09a480d3a0b40fe86c66a321d81b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831439"
---
# <a name="repudiation"></a>否认


## <span id="ddk_repudiation_if"></span><span id="DDK_REPUDIATION_IF"></span>


抵赖的概念是用户可能会执行特定操作，随后会拒绝执行该操作。 对于大多数驱动程序，这是一种异常类型的问题。 但对于文件系统，日志记录用于跟踪 (删除重要文件的操作，例如) 并确保操作的清晰跟踪。 这提供了一种机制来确保此类抵赖。

此外，操作系统还可以将对象的所有权分配给特定的安全标识符。 如果没有适当的权限，则无法更改所有权信息 (**SeTakeOwnershipPrivilege**) ，以确保能够跟踪特定对象的所有权。 对象所有权针对抵赖提供另一种形式的保护。

 

 




