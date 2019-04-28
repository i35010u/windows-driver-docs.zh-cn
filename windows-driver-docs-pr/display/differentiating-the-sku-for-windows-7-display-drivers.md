---
title: 区分 Windows 7 显示驱动程序的 SKU
description: 区分 Windows 7 显示驱动程序的 SKU
ms.assetid: 3cf72bd5-21bc-4a7f-8c2f-98f8e70d8248
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1222b8231372d251dabb72d6e010dd8aa483b216
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342406"
---
# <a name="differentiating-the-sku-for-windows-7-display-drivers"></a>区分 Windows 7 显示驱动程序的 SKU


所有 Windows Server 2008 中的框中显示驱动程序 INF 文件、 Windows Vista SP1 和更高版本中必须都包含一个值，指示的驱动程序是为仅限 Windows 客户端版本和在于不安装在 Windows 服务器 Sku 上。

在 Windows 7、 Windows Vista SP1、 Windows Server 2008 和 Windows Server 2008 R2**制造商**指令后面必须跟采用以下形式的字符串：

```inf
NT<platform>...1 
```

在此字符串中，平台为 x86 或 amd64。

下面的示例演示**制造商**指令，以及适用于 x86 的驱动程序后面的部分系统：

```inf
[Manufacturer]
%ATI% = ATI.Mfg,NTx86...1

[ATI.Mfg.NTx86...1]
```

下面的示例演示**制造商**指令，并针对 x64 的驱动程序后面的部分系统：

```inf
[Manufacturer]
%ATI% = ATI.Mfg,NTamd64...1

[ATI.Mfg.NTamd64...1]
```

有关详细信息**制造商**部分中，请参阅[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)。

 

 





