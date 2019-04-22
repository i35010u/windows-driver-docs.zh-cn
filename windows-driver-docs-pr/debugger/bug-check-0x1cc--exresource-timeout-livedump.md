---
title: Bug 检查 1CC EXRESOURCE_TIMEOUT_LIVEDUMP
description: EXRESOURCE_TIMEOUT_LIVEDUMP bug 检查具有 0x000001CC 值。
keywords:
- Bug 检查 0x1CC EXRESOURCE_TIMEOUT_LIVEDUMP
- EXRESOURCE_TIMEOUT_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- EXRESOURCE_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1231e2732924fa118b67ec0c90d25cc8ae941926
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238970"
---
# <a name="bug-check-bug-check-0x1cc-exresourcetimeoutlivedump"></a>Bug 检查 Bug 检查 0x1CC:EXRESOURCE\_超时\_LIVEDUMP

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


EXRESOURCE_TIMEOUT_LIVEDUMP bug 检查具有 0x000001CC 值。

内核 ERESOURCE 已超时。这可能指示死锁条件或这可能导致性能问题的大量争用。


## <a name="exresourcetimeoutlivedump-parameters"></a>EXRESOURCE\_超时\_LIVEDUMP 参数

在蓝色屏幕上显示以下参数。

参数 | 描述 
|---------|--------------|
1 | ERESOURCE 已超时。
2 | 检测到超时线程
3 | ERESOURCE 争用计数
4 | 配置的超时 （秒）


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

