---
title: C30032
description: 警告 C30032 调用内存分配函数，并通过使用 POOL_NX_OPTOUT 指令强制执行可执行内存请求。
ms.assetid: 7C6F9ACE-DD02-45A7-A601-C5C7A5C89256
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30032
ms.openlocfilehash: 3f8eae0b25bf202e07fda5f10ff6406520e6396f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381639"
---
# <a name="c30032"></a>C30032


警告 C30032：通过使用 [POOL \_ NX \_ 选择](../kernel/selective-opt-out-pool-nx-optout.md) 指令调用内存分配函数并强制执行可执行内存请求

禁止的 \_ 内存 \_ 分配 \_ 强制 \_ 不安全

预处理器指令 [池 \_ NX \_ 选择](../kernel/selective-opt-out-pool-nx-optout.md) 阻止将非安全类型 (**MM \_ 页面 \_ 优先级** 和 **池 \_ 类型**) 自动升级到安全类型 (例如，非分页池 to NonPagedPoolNx) 。 \_ \_ 在源中使用 POOL NX 选择可能是设计使然。 如果这是设计使然并且需要可执行内存，则可以使用 [杂注 Prefast 禁止显示警告消息](/previous-versions/windows/embedded/gg155764(v=winembedded.70))。 在已选择额外内存保护的 Windows 10 系统上不允许此类型的分配。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码将生成此警告：

在源文件中：

```
C_DEFINES=$(C_DEFINES) –DUNICODE -DPOOL_NX_OPTOUT=1
```

在代码文件中：

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

下面的代码可避免此警告：

在源文件中，添加：

```
C_DEFINES=$(C_DEFINES) -DUNICODE -DPOOL_NX_OPTIN_AUTO=1
```

在代码文件中：

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

 

