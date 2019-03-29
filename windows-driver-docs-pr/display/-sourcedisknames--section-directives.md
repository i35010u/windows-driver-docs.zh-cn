---
title: '[SourceDiskNames] 部分指令'
description: Windows Vista 及更高版本，在框 Inf 使用 [SourceDisksXxx] 指令。
ms.assetid: 0AC01548-3E53-41ED-9C7E-E33FC2DD14FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3058ea992a1f6c4809369d30783ab7e69e385acf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562271"
---
# <a name="sourcedisknames-section-directives"></a>\[SourceDiskNames\]部分指令


Windows Vista 及更高版本，内置使用 Inf *\[SourceDisksXxx\]* 指令。 但是，这些部分的值已从内容具有先前通常已记下独立硬件供应商 (IHV) 生产驱动程序包中更改。

## <a name="span-idsourcedisksnamesandsourcedisksfilessectiondirectivesspanspan-idsourcedisksnamesandsourcedisksfilessectiondirectivesspanspan-idsourcedisksnamesandsourcedisksfilessectiondirectivesspansourcedisksnames-and-sourcedisksfiles-section-directives"></a><span id="_SourceDisksNames__and__SourceDisksFiles__section_directives"></span><span id="_sourcedisksnames__and__sourcedisksfiles__section_directives"></span><span id="_SOURCEDISKSNAMES__AND__SOURCEDISKSFILES__SECTION_DIRECTIVES"></span>*\[SourceDisksNames\]* 并*\[SourceDisksFiles\]* 部分指令


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

## <a name="span-idsignatureattributessectiondirectivesspanspan-idsignatureattributessectiondirectivesspanspan-idsignatureattributessectiondirectivesspansignatureattributes-section-directives"></a><span id="_SignatureAttributes__section_directives"></span><span id="_signatureattributes__section_directives"></span><span id="_SIGNATUREATTRIBUTES__SECTION_DIRECTIVES"></span>*\[SignatureAttributes\]* 部分指令


Windows Vista 及更高版本，使用收件箱 Inf *\[SignatureAttributes\]* 指令。

没有必要引用的微型端口 (.sys) 文件。

例如：

``` syntax
[SignatureAttributes]
IHVUMD1.dll=SignatureAttributes.PETrust
IHVUMD2.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

 

 





