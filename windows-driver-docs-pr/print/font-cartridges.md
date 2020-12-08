---
title: 字体盒
description: 字体盒
keywords:
- 打印机字体说明 WDK Unidrv、盒式磁带
- 字体盒式 WDK Unidrv
- 字体盒式 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6867dc02aeef892a5ab4720c2527529311b5a38b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797073"
---
# <a name="font-cartridges"></a>字体盒





如果打印机接受字体盒，则可以通过 \* **FontCartridge** GPD 文件项来描述墨盒。 此项的格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* FontCartridge： <em>CartridgeName</em> {<em>FontCartidgeAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

其中， *CartridgeName* 是表示磁带名称的文本字符串， *FontCartridgeAttributes* 是一个或多个 [字体盒属性](font-cartridge-attributes.md)的集合。

或者，可以使用 [Unidrv 字体格式文件](customized-font-management.md#ddk-unidrv-font-format-files-gg) 指定字体盒提供的字体)  (. uff 文件。 通常，在 GPD 文件中描述最常提供的字体盒，而不太常用的墨盒则使用 uff 文件指定。

 

 




