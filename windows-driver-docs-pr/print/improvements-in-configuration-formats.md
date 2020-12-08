---
title: 配置格式的改进
description: V4 打印机驱动程序中的配置格式已经过改进，可以控制复制计数和标点替换。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 176430fa3a4868063344c4c60362d1a6a5e7976c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835719"
---
# <a name="improvements-in-configuration-formats"></a>配置格式的改进


V4 打印机驱动程序中的配置格式已经过改进，可以控制复制计数和标点替换。

**复制计数**

如果基于 GPD 的打印机驱动程序使用的是 XPS 到 PCL6 呈现筛选器，但不支持硬件副本，则它必须指定 **\* HardwareCopies** 指令来实现对副本计数的控制。 如果指令设置为 ON 或未指定，则会指示筛选器将硬件副本的相应 PCL6 命令发送到设备，以处理多个副本。 否则，如果指令设置为 OFF，则筛选器将生成软件副本。

**无标点替换**

由于使用 v3 打印机驱动程序的历史实现，某些设备可能需要标点符号（如句点 (）。 ) 或要在 PrintCapabilities 和 PrintTicket 实现中使用的连字符 ( ) 。 默认行为是将继续进行字符替换。 若要配置标点字符替换，请指定以下根级别属性：

| 文件类型 | 指令                      | 所需的值 |
|-----------|--------------------------------|----------------|
| GPD       | \*NoPunctuationCharSubstitute? | 正确           |
| 信息库       | \*MSPunctuationCharSubstitute  | 正确           |

 

## <a name="related-topics"></a>相关主题
[V4 驱动程序配置](v4-driver-configuration.md)  



