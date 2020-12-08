---
title: Bug 检查 0x16E ERESOURCE_INVALID_RELEASE
description: ERESOURCE_INVALID_RELEASE bug 检查的值为0x0000016E。 这表示提供给 ExReleaseResourceForThreadLite 的目标线程指针无效。
keywords:
- Bug 检查 0x16E ERESOURCE_INVALID_RELEASE
- ERESOURCE_INVALID_RELEASE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ERESOURCE_INVALID_RELEASE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8cfd0caec5cf4fdb777bcaabaab2caa7176b11ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791651"
---
# <a name="bug-check-0x16e-eresource_invalid_release"></a>Bug 检查0x16E： ERESOURCE \_ 无效 \_ 发布


ERESOURCE \_ 无效 \_ 发布 bug 检查的值为0x0000016E。 这表示提供给 ExReleaseResourceForThreadLite 的目标线程指针无效。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="eresource_invalid_release-parameters"></a>ERESOURCE \_ 无效的 \_ 发布参数


| 参数 | 描述                                    |
|-----------|------------------------------------------------|
| 1         | 正在释放的资源                    |
| 2         | 当前线程                             |
| 3         | 传入的错误目标线程 |
| 4         | 预留                                       |

 

<a name="cause"></a>原因
-----

如果 API 客户端跳过了对 ExSetOwnerPointerEx 的调用，则会命中此错误检查， (如果) 使用跨线程版本，或者如果调用方意外传入了 ExGetCurrentResourceThread 提供的值，则会发生此错误。

 

 




