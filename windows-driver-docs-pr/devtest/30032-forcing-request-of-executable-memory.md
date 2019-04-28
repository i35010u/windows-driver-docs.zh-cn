---
title: C30032
description: 警告 C30032 调用内存分配函数和强制执行内存通过使用 POOL_NX_OPTOUT 指令的请求。
ms.assetid: 7C6F9ACE-DD02-45A7-A601-C5C7A5C89256
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30032
ms.openlocfilehash: b658f105c35b48c3e3bae54a75fb6894323cd949
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347043"
---
# <a name="c30032"></a>C30032


警告 C30032:调用内存分配函数和强制执行内存使用请求[池\_NX\_OPTOUT](https://msdn.microsoft.com/library/windows/hardware/hh920401)指令

已禁止\_内存优化\_分配\_强制\_UNSAFE

预处理器指令[池\_NX\_OPTOUT](https://msdn.microsoft.com/library/windows/hardware/hh920401)阻止非安全类型的自动升级 (**MM\_页\_优先级**和**池\_类型**) 安全类型 （例如，非分页池到 NonPagedPoolNx）。 使用的池\_NX\_OPTOUT 中你的源是可能的设计。 如果这是设计使然，并且可执行文件的内存是必需的则可以禁止显示警告，其中包含[禁止显示警告消息的杂注 Prefast](https://msdn.microsoft.com/library/gg155764.aspx)。 在具有中选择更多的内存保护功能的 Windows 10 系统上不允许这种类型的分配。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码生成此警告：

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

 

 





