---
title: 配置格式的改进
description: V4 打印机驱动程序中的配置格式已经过改进，允许控制复制计数和标点符号的替换项。
ms.assetid: 66FC6BAF-26DD-4E18-B8C9-0BF494346917
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c02b747e7f86229cea1fb608cf23178d474553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390577"
---
# <a name="improvements-in-configuration-formats"></a>配置格式的改进


V4 打印机驱动程序中的配置格式已经过改进，允许控制复制计数和标点符号的替换项。

**份数**

如果基于 GPD 的打印机驱动程序使用 XPS PCL6 呈现筛选器，但不支持硬件副本，它必须指定 **\*HardwareCopies**指令来实现对副本计数的控制。 如果指令为设置为 ON，或未指定，这会指示筛选器将硬件副本的相应 PCL6 命令发送到设备，以处理多个副本。 否则，如果指令设置为 OFF，该筛选器将生成的软件副本。

**没有标点替换项**

由于历史实现中使用 v3 打印机驱动程序，而某些设备可能需要如句点 （.） 或连字符 （-） 用于 PrintCapabilities 和 PrintTicket 实现标点字符。 默认行为是字符替换项将继续进行。 若要配置标点字符代替，指定以下、 根级别的特性：

| 文件类型 | 指令                      | 所需的值 |
|-----------|--------------------------------|----------------|
| GPD       | \*NoPunctuationCharSubstitute? | True           |
| PPD       | \*MSPunctuationCharSubstitute  | True           |

 

## <a name="related-topics"></a>相关主题
[V4 驱动程序配置](v4-driver-configuration.md)  



