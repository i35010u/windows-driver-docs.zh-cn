---
title: ComputerHardwareIds 输出
description: ComputerHardwareIds 输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5cc9dc881ec8a061945014b189cb1cbd96ddd63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837807"
---
# <a name="computerhardwareids-output"></a>ComputerHardwareIds 输出


下面是 ComputerHardwareIds 工具生成的输出示例：

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

在此示例中，供应商 (Contoso Inc. ) 通常会将第二个硬件 ID (d7be59e5-29b5-589a-b49d-de7265ef6a7b) 用于供应商设备元数据包的 [PACKAGEINFO XML 文档](../install/packageinfo-xml-document.md)中的 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))元素的值。

 

