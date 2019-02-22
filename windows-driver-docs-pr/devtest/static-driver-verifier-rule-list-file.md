---
title: Static Driver Verifier 规则列表文件
description: Static Driver Verifier 规则列表文件
ms.assetid: 941df64c-b66b-4e7b-b340-9ef6b57d895d
keywords:
- 静态驱动程序验证程序 WDK，输入文件
- StaticDV WDK 输入文件
- SDV WDK 输入文件
- 输入文件 WDK Static Driver Verifier
- 文件 WDK Static Driver Verifier
- 规则 WDK Static Driver Verifier
- 文件的规则列表 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa8da1ae137057ab2f609acf2edb7f919c6246e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521568"
---
# <a name="static-driver-verifier-rule-list-file"></a>Static Driver Verifier 规则列表文件


SDV 规则列表文件是一个文本文件，其中列出了一个或多个[Static Driver Verifier 规则](https://msdn.microsoft.com/library/windows/hardware/ff551714)或规则名称模式，其中一条规则或规则在每一行上的名称模式。 这些规则可以按任意顺序显示，且它们验证它们出现的顺序。 文件扩展名为.sdv 文件，如 Test.sdv。

每个行列出该条例可在一个规则的名称，也可以是通配符 (\*)，它表示所有 SDV 规则。

SDV 包括有用的规则列表中的文件的一组\\工具\\sdv\\示例\\规则\_设置\\wdm 子目录的 WDK 和您可以创建你自己。

若要使用在命令中的规则列表文件，请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。

通常情况下，会使用规则列表文件可指定多个规则不能指定规则名称模式的 SDV 验证。 还有用于批处理和回归测试。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的示例规则列表文件列出了一套所选的 SDV 规则。

```
AddDevice
IrqlApcLte
LowerDriverReturn
KeWaitDeadlock
ZwRegistryOpen
```

以下命令使用规则的列表文件，MyRules.sdv，若要启动 SDV 验证。

```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\MyRules.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>注释

若要列出的验证规则而创建的规则列表文件具有.sdv 文件扩展名。 有关规则的 SDV 源代码文件扩展名为.slic 文件名称。

 

 





