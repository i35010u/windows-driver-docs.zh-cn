---
title: Bug 检查 0x58 FTDISK_INTERNAL_ERROR
description: FTDISK_INTERNAL_ERROR bug 检查的值为0x00000058。 如果系统是从镜像分区的错误副本启动的，则会发出此错误。
keywords:
- Bug 检查 0x58 FTDISK_INTERNAL_ERROR
- FTDISK_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FTDISK_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4e89e7686550530689017ed41d73c734bb5cd25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791997"
---
# <a name="bug-check-0x58-ftdisk_internal_error"></a>Bug 检查0x58： FTDISK \_ 内部 \_ 错误


FTDISK \_ 内部 \_ 错误 bug 检查的值为0x00000058。 如果系统是从镜像分区的错误副本启动的，则会发出此错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="ftdisk_internal_error-parameters"></a>FTDISK \_ 内部 \_ 错误参数


无

<a name="cause"></a>原因
-----

配置单元指示镜像有效，但不是。 配置单元实际上应指向卷影分区。

这几乎始终是由正在恢复的主分区导致的。

<a name="resolution"></a>解决方法
----------

从卷影分区重新启动系统。

 

 




