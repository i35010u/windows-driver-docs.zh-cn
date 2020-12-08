---
title: Bug 检查 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
description: REGISTRY_FILTER_DRIVER_EXCEPTION bug 检查的值为0x00000135。 此错误检查是由注册表筛选驱动程序中的未经处理的异常导致的。
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
ms.openlocfilehash: 0ebb3ff6221b74af46282dc5d7485ad29a7df388
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838833"
---
# <a name="bug-check-0x135-registry_filter_driver_exception"></a>Bug 检查0x135：注册表 \_ 筛选器 \_ 驱动程序 \_ 异常


注册表 \_ 筛选器 \_ 驱动程序 \_ 异常 bug 检查的值为0x00000135。 此错误检查是由注册表筛选驱动程序中的未经处理的异常导致的。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="registry_filter_driver_exception-parameters"></a>注册表 \_ 筛选器 \_ 驱动程序 \_ 异常参数


| 参数 | 描述                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 异常代码                                                           |
| 2         | 导致错误检查的异常的上下文记录的地址 |
| 3         | 驱动程序的回调例程地址                                    |
| 4         | 预留                                                                 |

 

<a name="cause"></a>原因
-----

此错误检测表明注册表筛选驱动程序未处理其通知例程中的异常。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 使用第三个参数确定有问题的驱动程序。

 

 




