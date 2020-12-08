---
title: 区分 Windows 7 显示驱动程序的 SKU
description: 区分 Windows 7 显示驱动程序的 SKU
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d68cdfdb6945c6e3822e218f0fcb3bb27806d9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809509"
---
# <a name="differentiating-the-sku-for-windows-7-display-drivers"></a>区分 Windows 7 显示驱动程序的 SKU


Windows Server 2008、Windows Vista SP1 和更高版本中的所有内置的显示驱动程序 INF 文件必须包含一个值，该值指示驱动程序仅适用于 Windows 客户端版本，而不是在 Windows Server Sku 上安装。

在 Windows 7、Windows Vista SP1、Windows Server 2008 和 Windows Server 2008 R2 中， **Manufacturer** 指令后面必须是以下形式的字符串：

```inf
NT<platform>...1 
```

在此字符串中，平台为 x86 或 amd64。

下面的示例显示了 **Manufacturer** 指令，以及用于 x86 系统驱动程序的以下部分：

```inf
[Manufacturer]
%ATI% = ATI.Mfg,NTx86...1

[ATI.Mfg.NTx86...1]
```

下面的示例显示了 **Manufacturer** 指令，并为 x64 系统的驱动程序提供了以下部分：

```inf
[Manufacturer]
%ATI% = ATI.Mfg,NTamd64...1

[ATI.Mfg.NTamd64...1]
```

有关 " **制造商** " 部分的详细信息，请参阅 [**INF 制造商部分**](../install/inf-manufacturer-section.md)。

 

