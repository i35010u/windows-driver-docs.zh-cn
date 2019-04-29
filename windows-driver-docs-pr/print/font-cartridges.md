---
title: 字体盒
description: 字体盒
ms.assetid: bc92e2eb-ea75-4f0f-85b7-1433d57401f3
keywords:
- 打印机字体说明 WDK Unidrv，盒式磁带
- 字体盒 WDK Unidrv
- 插件字体 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f64d4221595535ea98167d82b1ef55a4a062178
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372108"
---
# <a name="font-cartridges"></a>字体盒





如果您的打印机接受字体盒，可通过描述墨盒\* **FontCartridge** GPD 文件条目。 此条目的格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* FontCartridge:<em>CartridgeName</em> {<em>FontCartidgeAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

其中*CartridgeName*是文本字符串，表示该插件的名称和*FontCartridgeAttributes*是一组的一个或多个[字体墨盒特性](font-cartridge-attributes.md)。

或者，提供的字体盒的字体可以使用指定[Unidrv 字体格式文件](customized-font-management.md#ddk-unidrv-font-format-files-gg)（.uff 文件）。 通常情况下，最常提供的字体盒描述在 GPD 文件中，而指定更少常用盒式磁带时使用.uff 文件。

 

 




