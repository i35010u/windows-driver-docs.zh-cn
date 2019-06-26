---
title: 自定义的 PDEV 结构
description: 自定义的 PDEV 结构
ms.assetid: e5c51b9a-5f73-4411-88d8-931981a8450c
keywords:
- 呈现 WDK 打印，PDEV 结构的插件
- PDEV WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7166e081757ccc3a8a64ed68da23ce39bf2451c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372388"
---
# <a name="customized-pdev-structures"></a>自定义的 PDEV 结构





呈现插件实现三个方法，以支持专用 PDEV 结构。 Unidrv 呈现插件必须实现以下方法：

[**IPrintOemUni::EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)

[**IPrintOemUni::DisablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-disablepdev)

[**IPrintOemUni::ResetPDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-resetpdev)

Pscript5 呈现插件必须实现以下方法：

[**IPrintOemPS::EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enablepdev)

[**IPrintOemPS::DisablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-disablepdev)

[**IPrintOemPS::ResetPDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-resetpdev)

PDEV 结构是一个通用的词条。 它表示一个专用的本地定义的结构，用于使用通过定义它的模块。 通常情况下，它用于存储物理设备特性。 每个打印机驱动程序和每个呈现的插件，定义其自己 PDEV 结构。 没有任何全局定义的类型"PDEV"结构。

 

 




