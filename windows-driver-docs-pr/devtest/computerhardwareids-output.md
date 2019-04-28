---
title: ComputerHardwareIds 输出
description: ComputerHardwareIds 输出
ms.assetid: 38a08dda-92db-4389-9c2c-91fe17a88051
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cadc25f122b2e3da31b3a1b30ce5c4553305011
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343106"
---
# <a name="computerhardwareids-output"></a>ComputerHardwareIds 输出


以下是 ComputerHardwareIds 工具生成的输出示例：

```
Using the BIOS to gather information

## Computer Information

BIOS Vendor: Contoso Inc.
BIOS Version string: A16
System BIOS Major Version: 6
System BIOS Minor Version: 0

System Manufacturer: Contoso Inc.
System Family: (null)
System ProductName: Contoso SYS01

Enclosure Type: Portable


Hardware IDs
------------
{346511cf-ccee-5c6d-8ee9-3c70fc7aae83}    <- Manufacturer + Family + ProductName + BIOS Vendor + BIOS Version + Major Version + Minor Version
{d7be59e5-29b5-589a-b49d-de7265ef6a7b}    <- Manufacturer + Family + ProductName
```

在此示例中，供应商 (Contoso Inc.) 将通常用于第二个硬件 ID (d7be59e5-29b5-589a-b49d-de7265ef6a7b) 的值[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)中的元素[PackageInfo XML 文档](https://msdn.microsoft.com/library/windows/hardware/ff549602)的供应商的设备元数据包。

 

 





