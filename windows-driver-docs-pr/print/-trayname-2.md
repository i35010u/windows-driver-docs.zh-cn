---
title: '\ TrayName\ (OutputBins)'
description: '\ TrayName\ (OutputBins)'
ms.assetid: efdb5ecb-3abc-4dfd-8087-7f4f3a938cf2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6343d495b0ed5f5b2803f6a81c61ed1c2b5240d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372887"
---
# <a name="trayname-outputbins"></a>\[TrayName\] (OutputBins)


架构路径：\\Printer.Finishing.OutputBins。\[TrayName\]

节点类型： 属性

说明： 出纸器 IHV 映射属性名称。 IHV 可以映射为输出 bin IHV 特定送纸器名称和从以下列表名称：

OutputBin1

OutputBin2

OutputBin*xx* (*xx*是一个正整数值)

TopBin

MiddleBin

BottomBin

LargeCapacityBin

FaceUpBin

FaceDownBin

MailboxBin

\[TrayName\]属性包含三个对子值：已安装、 容量和级别。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 安装

架构路径：\\Printer.Finishing.OutputBins。\[TrayName\]： 安装

节点类型： 值

数据类型： BIDI\_BOOL

说明： 确定引用 bin \[TrayName\]设备上安装。 如果 **，则返回 TRUE**，该 bin 设备上安装了; 如果**FALSE**，在设备上未安装该 bin。

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 容量

架构路径：\\Printer.Finishing.OutputBins。\[TrayName\]： 容量

节点类型： 值

数据类型： BIDI\_INT

说明： 中表的当前引用的输出 bin 的容量。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> 级别

架构路径：\\Printer.Finishing.OutputBins。\[TrayName\]： 级别

节点类型： 值

数据类型： BIDI\_INT

说明： 的以百分比表示的当前引用的输出纸盒中剩余的容量。 完整的送纸器具有的值为 100，而空的送纸器具有值为 0。 如果级别不是可衡量的则返回值为-1 （表示未知的级别）。

 

 




