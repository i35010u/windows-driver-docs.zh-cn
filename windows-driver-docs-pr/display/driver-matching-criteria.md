---
title: 驱动程序匹配条件
description: 本主题描述用于选择驱动程序的最佳匹配项的元素。
ms.assetid: C41549AE-3FE0-44E8-9D45-1ED1124D010B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9d1cdf1aa92f3a285cf05c956994011f4953d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380099"
---
# <a name="driver-matching-criteria"></a>驱动程序匹配条件


本主题描述用于选择驱动程序的最佳匹配项的元素。

使用下列元素来选择驱动程序的最佳匹配项。 从最重要到最不重要的顺序列出它们：

1.  签名
    1.  签名
    2.  无符号

2.  范围
    1.  指定的
    2.  基本-DNF\_BASIC\_驱动程序

3.  签名分数
    1.  在签名
        1.  \#定义 SIGNERSCORE\_徽标\_高级 0x0D000001
        2.  \#定义 SIGNERSCORE\_徽标\_标准 0x0D000002
        3.  \#定义 SIGNERSCORE\_收件箱 0x0D000003
        4.  \#定义 SIGNERSCORE\_未分类 0x0D000004 / / 未分类 = = 收件箱 = = 标准 = = 高级时 SIGNERSCORE\_掩码筛选器应用
        5.  \#定义 SIGNERSCORE\_WHQL 0x0D000005 / /base WHQL。
        6.  \#定义 SIGNERSCORE\_AUTHENTICODE 0x0F000000

    2.  在无符号
        1.  \#定义 SIGNERSCORE\_0x80000000 未签名
        2.  \#定义 SIGNERSCORE\_W9X\_可疑 0xC0000000
        3.  \#定义 SIGNERSCORE\_未知的 0xFF000000

4.  功能分数，以显示
    1.  Windows 8 WHQL E0
    2.  Windows 8 的预发布版本驱动程序版 E3
    3.  Windows 7 WHQL E6
    4.  Windows 7 的收件箱 EC
    5.  Windows Vista WHQL F6
    6.  Windows Vista 收件箱 F8
    7.  Microsoft 基本显示驱动程序 FB
    8.  XDDM 第三方光纤通道 （在 Windows 8 中未使用）
    9.  XDDM 收件箱中 Windows Vista （未在 Windows 8 中使用）
    10. VGA FE （未在 Windows 8 中使用）
    11. 默认值或没有分数 FF
    12. 未签名驱动程序 FF
    13. 没有功能评分 FF

5.  匹配类型 (作为描述模型部分下显示 INF 匹配项 = 安装部分，HWID，CompatID。 使用 0 或 1 的硬件 Id 和个或多个 CompatIDs）
    1.  设备硬件 Id = = INF 硬件 Id
    2.  设备硬件 Id = = INF CompatID
    3.  设备 CompatID = = INF 硬件 Id
    4.  Device CompatID == INF CompatID

6.  匹配排名： 中的匹配项从设备列表匹配项的优先级
7.  驱动程序日期
8.  驱动程序的版本号

 

 





