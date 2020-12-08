---
title: SKU 差分指令
description: 对于 Windows Server 2008 和 Windows Vista SP1，已修改内置的显示驱动程序 Inf，使其包含仅将驱动程序表示为客户端的新值，也就是说，驱动程序将不会安装在 Windows 的服务器 Sku 上。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0313dcb71af9f34b913530b4d722bc9f162153e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793859"
---
# <a name="sku-differentiation-directive"></a>SKU 差分指令


对于 Windows Server 2008 和 Windows Vista SP1，已修改内置的显示驱动程序 Inf，使其包含仅将驱动程序表示为 *客户端* 的新值，也就是说，驱动程序将不会安装在 Windows 的服务器 sku 上。 Windows 8 中的所有显示器驱动程序都需要此指令。

在 SP1 之前的 Windows Vista 中，使用了以下值：

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

对于 Windows 8，将使用 Windows Vista SP1 和 Windows Server 2008 所用的相同值。

## <a name="span-idsku_differentiation_for_device_drivers__spanspan-idsku_differentiation_for_device_drivers__spanspan-idsku_differentiation_for_device_drivers__spansku-differentiation-for-device-drivers"></a><span id="SKU_differentiation_for_device_drivers__"></span><span id="sku_differentiation_for_device_drivers__"></span><span id="SKU_DIFFERENTIATION_FOR_DEVICE_DRIVERS__"></span>设备驱动程序的 SKU 差异


独立硬件供应商 (Ihv) 可以使用 ProductType INF 值来指示给定 INF 对于服务器或客户端平台仅有效。 这适用于 Windows XP 及更高版本的操作系统，并且更改相对简单，可实现。

因此，即使服务器系统的驱动程序存储中存在仅限客户端的驱动程序包，也无法安装该驱动程序。

[**INF 制造商部分**](../install/inf-manufacturer-section.md)主题显示了如何添加 *TargetOSVersion* ，以根据各种标准筛选设备安装。 其中一个条件是 *ProductType*，可用于指定可在其上安装包的 sku 类别。 为 *ProductType* 定义了以下值：

``` syntax
0x0000001 (VER_NT_WORKSTATION)
0x0000002 (VER_NT_DOMAIN_CONTROLLER)
0x0000003 (VER_NT_SERVER) 
```

对于任何指定的体系结构，都采用以下方法将典型 INF 修饰为在任何 SKU 上安装：

``` syntax
[Manufacturer]
%MSFT%=Models,amd64

[Models.NTamd64]
<models entries>
```

若要将此 INF 限制为仅在客户端上安装，需要将 "1" 的 ProductType 添加到修饰。 该数字可以表示为十进制或十六进制。 该文档显示十六进制，但为了简单起见，我将在示例中使用小数。

``` syntax
[Manufacturer]
%MSFT%=Models,amd64...1

; models section for workstation
[Models.NTamd64...1]
<models entries>
```

对于服务器，语法会将其中断，以便在客户端和普通服务器上安装。 其中每个都有其自己的产品类型。 遗憾的是，INF 语法要求您同时指定这两者以涵盖这两种情况。 因此，您需要复制整个模型部分，以真正涵盖服务器 SKU：

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

 

