---
title: 正确定位磁盘映像
description: 正确定位磁盘映像
ms.assetid: 7AC7DDDB-CDA3-4D0D-8D23-7BBA03536195
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db687b22b17ba2c2702231fc0c299903b87c5d07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563200"
---
# <a name="locating-disk-images-correctly"></a>正确定位磁盘映像


磁盘映像和卷管理工具必须了解何处使用 Volsnap 创建的快照时查找磁盘上的图像数据区域和对用户数据的影响。 磁盘映像的位置不正确时，快照将包含损坏的数据。

某些映像的产品进行了错误的假设，在磁盘上 BIOS 参数块 (BPB) 仅为 4k 个字节时事实上它将始终将扩展到磁盘的第一个 8k 字节。 结果，具体取决于卷的群集大小，如果映像工具查找用户数据在最后一个 4k 字节一部分 BPB，它可以导致数据丢失后的卷创建 Volsnap 快照。 这是由于映像工具放置在磁盘保留区域中的用户数据。

设置设备，如 512 个字节或 4k 字节逻辑扇区大小不会确定 BPB 的大小，因为它始终是为 8k 字节。

下表介绍的扇区布局和字节偏移量的要求数据区域的磁盘映像。

BCB 保留区域图像数据区域 （512 字节扇区） 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 + 0 （的字节偏移量） 4096 8192
 

 

 




