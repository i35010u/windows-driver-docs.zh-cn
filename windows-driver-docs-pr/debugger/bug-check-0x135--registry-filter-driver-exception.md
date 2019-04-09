---
title: Bug 检查 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
description: REGISTRY_FILTER_DRIVER_EXCEPTION bug 检查具有 0x00000135 值。 此检测错误被因注册表筛选驱动程序中未经处理的异常。
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
ms.openlocfilehash: d9989f43fa9311f9bb695335f587075de2f8076a
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238384"
---
# <a name="bug-check-0x135-registryfilterdriverexception"></a>Bug 检查 0x135：注册表\_筛选器\_驱动程序\_异常


注册表\_筛选器\_驱动程序\_异常错误检查的值为 0x00000135。 此检测错误被因注册表筛选驱动程序中未经处理的异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="registryfilterdriverexception-parameters"></a>注册表\_筛选器\_驱动程序\_异常参数


| 参数 | 描述                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 异常代码                                                           |
| 2         | 引发执行错误检查的上下文记录的地址 |
| 3         | 驱动程序的回调例程地址                                    |
| 4         | 保留                                                                 |

 

<a name="cause"></a>原因
-----

此检测错误指示注册表筛选驱动程序不处理其通知例程中的异常。

<a name="resolution"></a>分辨率
----------

通过使用第三个参数标识有问题的驱动程序。

 

 




