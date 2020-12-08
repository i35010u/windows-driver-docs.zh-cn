---
title: 存储类内存术语表
description: 词汇表页面
Robots: noindex, nofollow
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d6ca861b2b8364e789752cdb57b07e5258b4917b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835241"
---
# <a name="storage-class-memory-glossary"></a>存储类内存术语表


## <a name="span-idstarts_with_aspanspan-idstarts_with_aspanspan-idstarts_with_aspana"></a><span id="starts_with_A"></span><span id="starts_with_a"></span><span id="STARTS_WITH_A"></span>的


<span></span>**中断**  
在 NVDIMM-N 模块上停止当前正在运行的操作的操作。

<span></span>**单臂**  
一种操作，用于启用或禁用在 NVDIMM-N 模块上保存操作的一个或多个触发器。

## <a name="span-idstarts_with_bspanspan-idstarts_with_bspanspan-idstarts_with_bspanb"></a><span id="starts_with_B"></span><span id="starts_with_b"></span><span id="STARTS_WITH_B"></span>B


<span></span>**Backup**  
将 DRAM 内容从 NVDIMM-N 模块 DRAM 保存到非易失性内存的过程。 如本文档中所述，支持能源的设备可以使用离散能量源来提供能量，以防电源丢失触发备份。

<span></span>**BIOS (基本输入/输出系统)**  
在加载和启动操作系统之前，主机使用此代码来初始化其硬件。

## <a name="span-idstarts_with_dspanspan-idstarts_with_dspanspan-idstarts_with_dspand"></a><span id="starts_with_D"></span><span id="starts_with_d"></span><span id="STARTS_WITH_D"></span>2-d


<span></span>**设备管理策略**  
一个能源源策略，其中的模块管理保存操作使用的能源来源。

## <a name="span-idstarts_with_espanspan-idstarts_with_espanspan-idstarts_with_espane"></a><span id="starts_with_E"></span><span id="starts_with_e"></span><span id="STARTS_WITH_E"></span>电邮


<span></span>**能源源 (ES)**  
一种设备，在保存操作期间能够将能源存储并提供给 NVDIMM-N 模块。

<span></span>**擦除**  
在 NVDIMM-N 模块的非易失性内存中删除以前保存的 DRAM 内容的操作。

## <a name="span-idstarts_with_fspanspan-idstarts_with_fspanspan-idstarts_with_fspanf"></a><span id="starts_with_F"></span><span id="starts_with_f"></span><span id="STARTS_WITH_F"></span>果


<span></span>**出厂默认值**  
一种操作，用于清除 NVDIMM-N 模块上的所有非易失性内存，并将可读取的寄存器重置为出厂默认值，但确定保修符合性所需的数据除外。 此操作不会影响模块上的固件。

<span></span>**固件操作**  
与更新 NVDIMM-N 模块上的固件相关的操作。

## <a name="span-idstarts_with_hspanspan-idstarts_with_hspanspan-idstarts_with_hspanh"></a><span id="starts_with_H"></span><span id="starts_with_h"></span><span id="STARTS_WITH_H"></span>高


<span></span>**主持人**  
安装了 NVDIMM-N 模块的系统。

<span></span>**主机管理策略**  
ES 策略，其中主机管理在 NVDIMM-N 模块的保存操作期间使用的 ES。

## <a name="span-idstarts_with_ispanspan-idstarts_with_ispanspan-idstarts_with_ispani"></a><span id="starts_with_I"></span><span id="starts_with_i"></span><span id="STARTS_WITH_I"></span>看到


<span></span>**I2c 总线 (集成线路)**  
一种双向双线总线，用于实现有效的集成线路控制。 NVDIMM-N 模块的当前设计使用 I i2c 总线。

## <a name="span-idstarts_with_nspanspan-idstarts_with_nspanspan-idstarts_with_nspann"></a><span id="starts_with_N"></span><span id="starts_with_n"></span><span id="STARTS_WITH_N"></span>北


<span></span>**NVDIMM-N**  
使用 NAND flash 提供持续 DRAM 的 NVDIMM 的 JEDEC 定义的术语。

## <a name="span-idstarts_with_rspanspan-idstarts_with_rspanspan-idstarts_with_rspanr"></a><span id="starts_with_R"></span><span id="starts_with_r"></span><span id="STARTS_WITH_R"></span>迅驰


<span></span>**Restore**  
将以前保存的 DRAM 内容从非易失性内存还原到 NVDIMM-N 模块的 DRAM 的过程。

## <a name="span-idstarts_with_sspanspan-idstarts_with_sspanspan-idstarts_with_sspans"></a><span id="starts_with_S"></span><span id="starts_with_s"></span><span id="STARTS_WITH_S"></span>些


<span></span>**把**  
断电时将 NVDIMM-N 的 DRAM 内容复制到非易失性内存的过程。 当发生启用的触发器时，将启动保存操作。

## <a name="span-idstarts_with_vspanspan-idstarts_with_vspanspan-idstarts_with_vspanv"></a><span id="starts_with_V"></span><span id="starts_with_v"></span><span id="STARTS_WITH_V"></span>向量


<span></span>**供应商日志页**  
模块上可由主机访问的可选区域，其中包含特定于供应商的数据，可用于在 NVDIMM-N 模块上诊断问题。

 

 





