---
title: 正确定位磁盘映像
description: 正确定位磁盘映像
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b311cd4c1832128fd653305b3e3186734d82da6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828783"
---
# <a name="locating-disk-images-correctly"></a>正确定位磁盘映像


磁盘映像和卷管理工具必须知道在何处查找磁盘上的映像数据区域，以及使用 Volsnap 创建的快照时对用户数据的影响。 如果磁盘映像的位置不正确，则快照将包含损坏的数据。

某些映像产品的假设是，BIOS 参数块 (磁盘上的 BPB) 只是4K 字节，实际上它将始终扩展到磁盘的第一个8K 字节。 因此，根据卷的群集大小，如果映像工具在 BPB 的最后一个4K 字节部分中查找用户数据，则在为卷创建 Volsnap 快照后，可能会导致数据丢失。 这是因为图像处理工具将用户数据置于磁盘的保留区域中。

为设备设置的逻辑扇区大小（如512字节或4K 字节）不确定 BPB 的大小，因为它始终是8K 字节。

下表描述了磁盘映像的数据区域的扇区布局和字节偏移量要求。

BCB 保留区域图像数据区域 0 (512 字节扇区) 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 + 0 (字节偏移) 4096 8192
 

 

 




