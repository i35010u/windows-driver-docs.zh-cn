---
title: Bug 检查 0x1A7 SMB_REDIRECTOR_LIVEDUMP
description: SMB_REDIRECTOR_LIVEDUMP bug 检查具有 0x000001A7 值。 它指示 SMB 重定向程序已检测到问题和已捕获核心转储收集调试信息。
keywords:
- Bug 检查 0x1A7 SMB_REDIRECTOR_LIVEDUMP
- SMB_REDIRECTOR_LIVEDUMP
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- SMB_REDIRECTOR_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d08ff98749d22d66a9ed60e98f503fc089986452
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866508"
---
# <a name="bug-check-0x1a7-smbredirectorlivedump"></a>Bug 检查 0x1A7：SMB\_重定向程序\_LIVEDUMP

SMB\_重定向程序\_LIVEDUMP bug 检查的值为 0x000001A7。 它指示 SMB 重定向程序已检测到问题和已捕获核心转储收集调试信息。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="smbredirectorlivedump-parameters"></a>SMB\_重定向程序\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 原因代码为-请参阅下面的值。|
|2| 请参阅下面的值。|
|3| 保留。|
|4| 保留。|

SMB 重定向程序检测到问题，并已捕获核心转储收集调试信息。

**原因代码**

```text
0x1 : An I/O failed to complete in a reasonable amount of time.
    2 - Pointer to the connection object.
    3 - Reserved.
    4 - Reserved.
```

## <a name="cause"></a>原因
-----

SMB 重定向程序检测到问题，并已捕获核心转储收集调试信息。

仅当设置以下注册表值，将生成此错误检查代码的实时转储。

```registry
HKLM\System\CurrentControlSet\Services\Lanmanworkstation\Parameters [DWORD] LiveDumpFilter = 1
```

当设置此注册表项和 io，RDR 可以超时，将发生 livedump。

（此代码可以永远不会用于实际的执行错误检查; 它用于标识实时转储）。

## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)
