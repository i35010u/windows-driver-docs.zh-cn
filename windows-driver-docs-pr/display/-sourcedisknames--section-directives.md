---
title: '[SourceDiskNames] 节指令'
description: 在 Windows Vista 和更高版本中，使用 [SourceDisksXxx] 指令。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d9fab22def998d6c6c7dab752c5f082c2fba7ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810603"
---
# <a name="sourcedisknames-section-directives"></a>\[SourceDiskNames \] 节指令


在 Windows Vista 和更高版本中，使用 *\[ SourceDisksXxx \]* 的 inf。 不过，这些部分的值已从先前通常在独立硬件供应商 (IHV) 生产驱动程序包中记录的内容进行了更改。

## <a name="span-id_sourcedisksnames__and__sourcedisksfiles__section_directivesspanspan-id_sourcedisksnames__and__sourcedisksfiles__section_directivesspanspan-id_sourcedisksnames__and__sourcedisksfiles__section_directivesspansourcedisksnames-and-sourcedisksfiles-section-directives"></a><span id="_SourceDisksNames__and__SourceDisksFiles__section_directives"></span><span id="_sourcedisksnames__and__sourcedisksfiles__section_directives"></span><span id="_SOURCEDISKSNAMES__AND__SOURCEDISKSFILES__SECTION_DIRECTIVES"></span>*\[ SourceDisksNames \]* 和 *\[ SourceDisksFiles \]* 节指令


例如，对于 IHV 生产驱动程序：

``` syntax
For example, IHV production drivers:
[SourceDisksNames]
1 = %DiskID1%

[SourceDisksFiles]
r200.sys    = 1
r200umd.dll = 1
```

这是 Windows 收件箱 INF 要求：

``` syntax
[SourceDisksNames]
3426=windows cd

[SourceDisksFiles]
IHVKDM.sys      = 3426
IHVUMD.dll      = 3426
IHVVID.dll      = 3426
```

## <a name="span-id_signatureattributes__section_directivesspanspan-id_signatureattributes__section_directivesspanspan-id_signatureattributes__section_directivesspansignatureattributes-section-directives"></a><span id="_SignatureAttributes__section_directives"></span><span id="_signatureattributes__section_directives"></span><span id="_SIGNATUREATTRIBUTES__SECTION_DIRECTIVES"></span>*\[ SignatureAttributes \]* 节指令


在 Windows Vista 和更高版本中，收件箱 Inf 使用 *\[ SignatureAttributes \]* 指令。

无需引用小型端口 ( .sys) 文件。

例如：

``` syntax
[SignatureAttributes]
IHVUMD1.dll=SignatureAttributes.PETrust
IHVUMD2.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

 

 





