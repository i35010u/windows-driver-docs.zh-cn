---
title: 完成
description: 完成
ms.assetid: 5c8e556b-102a-4caf-92d3-8b61bec1a29f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c48599392268cb6ff9fdd8be68c9a43ab813a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542838"
---
# <a name="finishing"></a>完成


架构路径：\\Printer.Finishing

节点类型： 属性

完成属性包含有关打印完成后执行的操作数据。 这包括是否可以调整文档，装订，打孔漏洞，以及可用纸盒的相关信息。

完成属性包含两个对子值 CollationSupported 和 JogOffsetSupported;它也是父[书钉](staple3.md)， [HolePunch](holepunch3.md)，并[OutputBins](outputbins2.md)属性。

### <a name="span-idcollationsupportedspanspan-idcollationsupportedspan-collationsupported"></a><span id="collationsupported"></span><span id="COLLATIONSUPPORTED"></span> CollationSupported

架构路径：\\Printer.Finishing:CollationSupported

节点类型： 值

数据类型： BIDI\_BOOL

说明： 指示打印机是否支持硬件的打印文档的排序规则。 如果 **，则返回 TRUE**，支持排序规则; 如果**FALSE**，不支持排序规则。

### <a name="span-idjogoffsetsupportedspanspan-idjogoffsetsupportedspan-jogoffsetsupported"></a><span id="jogoffsetsupported"></span><span id="JOGOFFSETSUPPORTED"></span> JogOffsetSupported

架构路径：\\Printer.Finishing:JogOffsetSupported

节点类型： 值

数据类型： BIDI\_BOOL

说明： 确定打印机是否支持在交错组中的输出纸盒中打印作业或单独的打印作业的置于单独的副本。 如果 **，则返回 TRUE**，打印机支持慢走偏移量; 如果**FALSE**，打印机不支持此功能。

 

 




