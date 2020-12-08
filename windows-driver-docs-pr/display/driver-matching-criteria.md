---
title: 驱动程序匹配条件
description: 本主题介绍用于选择驱动程序的最佳匹配项的元素。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5b83893f9680b5f52eb957e3f3b6909e357a1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809152"
---
# <a name="driver-matching-criteria"></a>驱动程序匹配条件


本主题介绍用于选择驱动程序的最佳匹配项的元素。

以下元素用于选择驱动程序的最佳匹配项。 它们按从最重要到最不重要的顺序列出：

1.  签名
    1.  有符号
    2.  无符号

2.  范围
    1.  特定
    2.  基本-DNF \_ 基本 \_ 驱动程序

3.  签名分数
    1.  在签名中
        1.  \#定义 SIGNERSCORE \_ 徽标 \_ PREMIUM 0x0D000001
        2.  \#定义 SIGNERSCORE \_ 徽标 \_ 标准0x0D000002
        3.  \#定义 SIGNERSCORE \_ 收件箱0x0D000003
        4.  \#\_在 \_ 应用 SIGNERSCORE 掩码筛选器时，定义 SIGNERSCORE 未分类 0x0D000004//非分类 = = 收件箱 = = STANDARD = = PREMIUM
        5.  \#定义 SIGNERSCORE \_ Whql 0x0D000005//BASE whql。
        6.  \#定义 SIGNERSCORE \_ AUTHENTICODE 0x0F000000

    2.  未签名
        1.  \#定义 SIGNERSCORE \_ 无符号0x80000000
        2.  \#定义 SIGNERSCORE \_ W9X \_ 可疑0xC0000000
        3.  \#定义 SIGNERSCORE \_ UNKNOWN 0xFF000000

4.  功能分数，用于显示
    1.  Windows 8 WHQL E0
    2.  Windows 8 预发行版驱动程序 E3
    3.  Windows 7 WHQL E6
    4.  Windows 7 收件箱 EC
    5.  Windows Vista WHQL F6
    6.  Windows Vista 收件箱 F8
    7.  Microsoft 基本显示器驱动程序 FB
    8.  Windows 8) 中未使用 XDDM 第三方 FC (
    9.  Windows Vista FD 中的 XDDM 收件箱 (在 Windows 8 中不使用) 
    10. Windows 8 中未使用的 VGA FE () 
    11. 默认或没有评分 FF
    12. 无符号驱动程序 FF
    13. 没有功能分数 FF

5.  匹配类型 (INF 匹配项在 "型号" 部分下列出，作为 Description = Install 部分，HWID，CompatID。 带有0个或1个 HW Id 以及0个或多个 CompatIDs) 
    1.  设备 HardwareID = = INF HardwareID
    2.  设备 HardwareID = = INF CompatID
    3.  设备 CompatID = = INF HardwareID
    4.  设备 CompatID = = INF CompatID

6.  匹配排名：从设备的匹配列表中匹配的优先级
7.  驱动程序日期
8.  驱动程序版本号

 

 





