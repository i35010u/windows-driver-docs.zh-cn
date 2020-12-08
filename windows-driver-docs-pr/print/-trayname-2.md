---
title: '\ TrayName \ (OutputBins) '
description: '\ TrayName \ (OutputBins) '
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa7d3302b4cc68b9f1e5c541eefff4226d81690b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806005"
---
# <a name="trayname-outputbins"></a>\[TrayName \] (OutputBins) 


架构路径： \\ OutputBins \[ 。TrayName\]

节点类型：属性

说明：输出栏的 IHV 映射属性名称。 IHV 可以使用以下列表中的名称映射特定于 IHV 的托盘名称：

OutputBin1

OutputBin2

OutputBin *xx* (*xx* 是正整数) 

TopBin

MiddleBin

BottomBin

LargeCapacityBin

FaceUpBin

FaceDownBin

MailboxBin

\[TrayName \] 属性包含三个子值：已安装、容量和级别。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 随

架构路径： \\ OutputBins \[ 。TrayName \] ：已安装

节点类型：值

数据类型：双向 \_ BOOL

说明：确定 \[ 设备上是否已安装 TrayName 引用的 bin \] 。 如果 **为 TRUE**，则将在设备上安装 bin;如果 **为 FALSE**，则不会在设备上安装该 bin。

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 功能

架构路径： \\ OutputBins \[ 。TrayName \] ：容量

节点类型：值

数据类型：双向 \_ INT

说明：当前所引用的输出箱的容量（以工作表为限）。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> 调配

架构路径： \\ OutputBins \[ 。TrayName \] ：级别

节点类型：值

数据类型：双向 \_ INT

说明：当前引用的输出箱中剩余的容量量，以百分比表示。 完全纸盒的值为100，而空的托盘的值为0。 如果级别不可度量，则值为-1 (指示应返回未知级别) 。

 

 




