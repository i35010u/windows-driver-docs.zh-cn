---
title: 通过指定值数据的使用情况来提取该值
description: 通过指定值数据的使用情况来提取该值
ms.assetid: 043cdb68-ead8-4ccf-ae00-1165fe2988f4
keywords:
- HID 报告 WDK，提取控制数据
- 报告 WDK HID，提取控件数据
- 提取 HID 控件数据
- 数据使用提取 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6c6982fb567b1ee0319a5d5411c94a123c3869a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824819"
---
# <a name="extracting-value-data-by-specifying-its-usage"></a>通过指定值数据的使用情况来提取该值





若要从 HID 报表中提取值数据，应用程序或驱动程序可以使用以下 HID 支持例程之一：

<a href="" id="hidp-getscaledusagevalue"></a>[**HidP\_GetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)  
返回已签名且缩放的值。

<a href="" id="hidp-getusagevalue"></a>[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)  
返回一个无符号格式的 nonscaled 值或超出其**正常**范围的缩放值。

<a href="" id="hidp-getusagevaluearray"></a>[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)  
返回使用情况值数组。

若要使用**HidP\_GetUsageValueArray**，应用程序和驱动程序必须分配一个零初始化缓冲区，该缓冲区的大小足以容纳用量值数组。 所需的大小（以字节为单位）是 BitSize 和 ReportCount 成员的和成员的积，其[**HIDP\_值\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)结构，向上舍入到最接近的字节。

 

 




