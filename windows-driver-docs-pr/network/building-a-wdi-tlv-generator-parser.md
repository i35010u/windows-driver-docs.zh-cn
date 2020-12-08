---
title: 将 WDI TLV 生成器/分析器添加到驱动程序
description: 若要将 WDI TLV 生成器/分析器添加到你的驱动程序，请执行以下步骤。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 420f7f554f7767b00995b5ce0eff50a2f5d3e1d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802363"
---
# <a name="adding-the-wdi-tlv-generatorparser-to-your-driver"></a>将 WDI TLV 生成器/分析器添加到驱动程序


若要将 WDI TLV 生成器/分析器添加到你的驱动程序，请执行以下步骤。

1.  将此包含在 dot11wdi 和 wditypes 之后。

    `#include "TlvGeneratorParser.hpp"`

2.  将此库添加到链接器。

    `TLVGeneratorParser.lib`

3.  定义、创建和写入内存 Api (重载运算符 new/delete) 。

4.  开始调用 Api。

 

 





