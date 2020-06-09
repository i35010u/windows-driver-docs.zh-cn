---
title: Bug 检查 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
description: REGISTRY_FILTER_DRIVER_EXCEPTION bug 检查的值为0x00000135。 此错误检查是由注册表筛选驱动程序中的未经处理的异常导致的。
ms.assetid: 99E171F4-5629-405F-993C-51287AD7D2C8
keywords:
- Bug 检查 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
- REGISTRY_FILTER_DRIVER_EXCEPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_FILTER_DRIVER_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 600cc492d8bfe619d20a80bf9b1ae81b371b7d90
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534660"
---
# <a name="bug-check-0x135-registry_filter_driver_exception"></a>Bug 检查0x135：注册表 \_ 筛选器 \_ 驱动程序 \_ 异常


注册表 \_ 筛选器 \_ 驱动程序 \_ 异常 bug 检查的值为0x00000135。 此错误检查是由注册表筛选驱动程序中的未经处理的异常导致的。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="registry_filter_driver_exception-parameters"></a>注册表 \_ 筛选器 \_ 驱动程序 \_ 异常参数


| 参数 | 说明                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 异常代码                                                           |
| 2         | 导致错误检查的异常的上下文记录的地址 |
| 3         | 驱动程序的回调例程地址                                    |
| 4         | 保留                                                                 |

 

<a name="cause"></a>原因
-----

此错误检测表明注册表筛选驱动程序未处理其通知例程中的异常。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 使用第三个参数确定有问题的驱动程序。

 

 




