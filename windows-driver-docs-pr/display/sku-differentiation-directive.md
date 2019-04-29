---
title: SKU 差分指令
description: 使用 Windows Server 2008 和 Windows Vista SP1，在框中显示驱动程序 Inf 已修改为包括一个新值，表示为仅客户端，这意味着将驱动程序将不在服务器 Sku 的 Windows 上安装的驱动程序。
ms.assetid: 9E31BD57-41B6-40DF-AF27-8EAC66BDFE09
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed938bf022119b792b43c78f51e82fcf18668717
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391231"
---
# <a name="sku-differentiation-directive"></a>SKU 差分指令


使用 Windows Server 2008 和 Windows Vista SP1 中，框中显示驱动程序 Inf 已修改为包括一个新值，表示作为驱动程序*客户端仅*，驱动程序将不在服务器 Sku 的 Windows 安装的含义。 此指令时在 Windows 8 中的所有显示器驱动程序的要求。

在 Windows Vista SP1 之前，使用以下值：

``` syntax
X86:
[Manufacturer]
%ATI% = ATI.Mfg

[ATI.Mfg]

In Vista SP1\Server 2008 the following values were used; 
X86:
[Manufacturer]
%ATI% = ATI.Mfg,NTx86...1

[ATI.Mfg.NTx86...1]

X64:
[Manufacturer]
%ATI% = ATI.Mfg,NTamd64...1

[ATI.Mfg.NTamd64...1]
```

对于 Windows 8 中，使用适用于 Windows Vista SP1 和 Windows Server 2008 使用的相同值。

## <a name="span-idskudifferentiationfordevicedriversspanspan-idskudifferentiationfordevicedriversspanspan-idskudifferentiationfordevicedriversspansku-differentiation-for-device-drivers"></a><span id="SKU_differentiation_for_device_drivers__"></span><span id="sku_differentiation_for_device_drivers__"></span><span id="SKU_DIFFERENTIATION_FOR_DEVICE_DRIVERS__"></span>SKU 差异化的设备驱动程序


独立硬件供应商 (Ihv) 可以使用 ProductType INF 值以指示给定的 INF 是有效的服务器或客户端平台。 此过程适用于 Windows XP 和更高版本的操作系统，并且这些更改将实现相对简单。

因此，即使某个服务器系统的驱动程序存储区中存在的客户端的驱动程序包，该驱动程序不是可安装。

[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)主题演示如何添加*TargetOSVersion*到筛选器基于各种条件的设备安装。 这些条件之一是*ProductType*，这可用于指定可以在其安装包的 Sku 的类别。 定义以下值*ProductType*:

``` syntax
0x0000001 (VER_NT_WORKSTATION)
0x0000002 (VER_NT_DOMAIN_CONTROLLER)
0x0000003 (VER_NT_SERVER) 
```

对于任何给定的体系结构，典型 INF 修饰上任何 SKU 安装如下所示：

``` syntax
[Manufacturer]
%MSFT%=Models,amd64

[Models.NTamd64]
<models entries>
```

为了限制客户端上安装此 INF 仅，需要将添加为"1"ProductType 到修饰。 可能为十进制或十六进制表示的数字。 此文档介绍十六进制的但我将在示例中为简单起见使用小数。

``` syntax
[Manufacturer]
%MSFT%=Models,amd64...1

; models section for workstation
[Models.NTamd64...1]
<models entries>
```

对于服务器，语法将分解它在客户端和普通服务器上安装。 每个具有其自己的产品类型。 遗憾的是 INF 语法要求你同时涵盖两种情况下指定。 因此，您需要重复整个的模型部分，以真正覆盖服务器 SKU:

``` syntax
[Manufacturer]
%MSFT%=Models,amd64...1amd64...3

; models section for client
[Models.NTamd64...1]
IHV_DeviceName.XXX = "Foo Generic Device Name (Microsoft Corporation - WDDM v1.2)"
IHV_DeviceName.YYY = "Foo Enthusiast Device Name (Microsoft Corporation - WDDM v1.2)"
<models entries>

; models section for Server
[Models.NTamd64...3]
IHV_DeviceName.XXX = "Foo Generic Name (Microsoft Corporation - WDDM v1.2)"
IHV_DeviceName.ZZZ = "Foo Datacenter Name (Microsoft Corporation - WDDM v1.2)"
<models entries>
```

 

 





