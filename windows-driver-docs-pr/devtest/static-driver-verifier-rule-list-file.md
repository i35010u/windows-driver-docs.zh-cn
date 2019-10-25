---
title: 静态驱动程序验证程序规则列表文件
description: 静态驱动程序验证程序规则列表文件
ms.assetid: 941df64c-b66b-4e7b-b340-9ef6b57d895d
keywords:
- 静态驱动程序验证程序 WDK，输入文件
- StaticDV WDK，输入文件
- SDV WDK，输入文件
- 输入文件 WDK 静态驱动程序验证程序
- 文件 WDK 静态驱动程序验证程序
- 规则 WDK 静态驱动程序验证程序
- 规则列表文件 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b65b925b8d6c87bafb0bcb7a7ac877efa54035fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839307"
---
# <a name="static-driver-verifier-rule-list-file"></a>静态驱动程序验证程序规则列表文件


SDV 规则列表文件是一个文本文件，该文件列出一个或多个[静态驱动程序验证程序规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)或规则名称模式，每一行上有一个规则或规则名称模式。 规则可以按任意顺序显示，并按它们出现的顺序进行验证。 文件的文件扩展名为 sdv，例如 sdv。

每行上列出的规则可以是一条规则的名称，也可以是通配符（\*），表示所有 SDV 规则。

SDV 在 \\工具中包含一组有用的规则列表文件\\SDV\\示例\\规则\_设置 WDK\\wdm 子目录，你可以创建自己的规则列表。

若要在命令中使用规则列表文件，请参阅[静态驱动程序验证程序命令（MSBuild）](-static-driver-verifier-commands--msbuild-.md)。

通常，您将使用规则列表文件为 SDV 验证指定多个规则，而不能使用规则名称模式来指定。 它对于批处理和回归测试也很有用。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

以下示例规则列表文件列出了一组选定的 SDV 规则。

```
AddDevice
IrqlApcLte
LowerDriverReturn
KeWaitDeadlock
ZwRegistryOpen
```

以下命令使用规则列表文件 MyRules. sdv 启动 SDV 验证。

```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\MyRules.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

### <a name="span-idcommentspanspan-idcommentspancomment"></a><span id="comment"></span><span id="COMMENT"></span>条

为列出验证规则而创建的规则列表文件的文件扩展名为 sdv。 规则的 SDV 源代码文件的文件扩展名为 slic。

 

 





