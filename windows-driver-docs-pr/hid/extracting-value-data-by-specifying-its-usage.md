---
title: 通过指定其使用情况数据的提取值
description: 通过指定其使用情况数据的提取值
ms.assetid: 043cdb68-ead8-4ccf-ae00-1165fe2988f4
keywords:
- HID 的报表 WDK，提取控件数据
- WDK HID，提取控件数据的报表
- HID 控制如何将数据提取
- 数据使用情况提取 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b1afadef2e51cf600b5f048a269843e3e2907e44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562157"
---
# <a name="extracting-value-data-by-specifying-its-usage"></a>通过指定其使用情况数据的提取值





若要从 HID 报表中提取值数据，应用程序或驱动程序可以使用下面的 HID 支持例程之一：

<a href="" id="hidp-getscaledusagevalue"></a>[**HidP\_GetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539729)  
返回一个已签名和缩放值。

<a href="" id="hidp-getusagevalue"></a>[**HidP\_GetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539748)  
返回非缩放值中的无符号的格式或缩放后的值超出其**正常**范围。

<a href="" id="hidp-getusagevaluearray"></a>[**HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)  
返回的使用情况值数组。

若要使用**HidP\_GetUsageValueArray**，应用程序和驱动程序必须分配足够大以保存使用情况值数组初始化为零的缓冲区。 所需的大小，以字节为单位，是的产品**BitSize**并**ReportCount**的使用情况值数组成员[ **HIDP\_值\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539832)结构，向上舍入到最接近的字节。

 

 




