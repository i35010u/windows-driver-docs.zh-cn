---
title: 当前设置
description: 当前设置
ms.assetid: 4de99ad0-fcd9-4f8d-8125-8f622443a0c6
keywords:
- 当前注册表设置 WDK 游戏杆
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aae5edf8cdb3b551bb776063c6cf8cc5f98e4d03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575546"
---
# <a name="current-settings"></a>当前设置





有两个部分： 当前的注册表设置： 若要存储，这是标准的轮询，并在其下存储的功能、 已校准的值和微型驱动程序数据的密钥的替换值。

可以在名为 REGSTR 密钥定义微型驱动程序用于轮询设备不具有关联的微型驱动程序来替换标准轮询\_VAL\_JOYCALLOUT。 此功能是 DirectX 3.0 的新增功能。 值由控制面板中设置高级的设置页时用户从包含所有有乐趣的微型驱动程序的列表中选择新的全局驱动程序\_工作流服务\_ISGAMEPORTDRIVER 标志设置。

其余设置存储在 REGSTR\_密钥\_JOYCURR 密钥。 当设备首次配置到特定游戏杆 ID 时，控制面板中值复制下 REGSTR 相关的 OEM 密钥\_路径\_JOYOEM 到 REGSTR\_密钥\_JOYCURR 密钥。 每个下此密钥的密钥值名称包含游戏杆 ID 作为名称的一部分，因此每个游戏杆都有其自己的设置。 REGSTR\_VAL\_JOYOEMNAME 值复制到相关 REGSTR\_VAL\_JOYNOEMNAME 和 （如果存在） REGSTR\_VAL\_JOYOEMCALLOUT 值复制到 REGSTR\_VAL\_JOYNOEMCALLOUT。 REGSTR\_VAL\_JOYOEMDATA 值用作前两个双字的 REGSTR\_VAL\_JOYNCONFIG 值，该值定义 （当展开时），如下所示的整体使用：

```cpp
struct {
    /* usage settings, copied from REGSTR_VAL_JOYOEMNAME */
    struct {
        DWORD   dwFlags;
        DWORD   dwNumButtons;
    } hws;
 
    /* usage flags, described below */
    DWORD    dwUsageSettings;
 
    struct {
        /* values returned by hardware during calibration */
        struct { 
            /* minimums for each axis */
            struct {
                DWORD    dwX;
                DWORD    dwY;
                DWORD    dwZ;
                DWORD    dwR;
                DWORD    dwU;
                DWORD    dwV;
            } jpMin;
            /* maximums for each axis */
            struct {
                DWORD    dwX;
                DWORD    dwY;
                DWORD    dwZ;
                DWORD    dwR;
                DWORD    dwU;
                DWORD    dwV;
            } jpMax;
            /* center positions for each axis */
            struct
            {
                DWORD    dwX;
                DWORD    dwY;
                DWORD    dwZ;
                DWORD    dwR;
                DWORD    dwU;
                DWORD    dwV;
            } jpCenter;
        } jrvHardware;
 
        /* POV values returned by hardware during calibration */
        DWORD   dwPOVValues[JOY_POV_NUMDIRS];
 
        /* calibration flags, described below */
        DWORD   dwCalFlags;
    } hwv; 
 
    /* type of joystick, described below */
    DWORD   dwType;
 
    /* reserved for OEM drivers */
    DWORD   dwReserved; 
};
```

使用情况设置是以下值的组合：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_US_HASRUDDER</p></td>
<td><p>0x00000001l</p></td>
<td><p>/ * 游戏杆使用舵配置 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_US_PRESENT</p></td>
<td><p>0x00000002l</p></td>
<td><p>/</em> 游戏杆是否真的存在？ <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_US_ISOEM</p></td>
<td><p>0x00000004l</p></td>
<td><p>/</em> 游戏杆是 OEM 定义的类型 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_US_RESERVED</p></td>
<td><p>0x80000000l</p></td>
<td><p>/</em> 保留 * /</p></td>
</tr>
</tbody>
</table>

 

校准标志是以下值的组合：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>JOY_ISCAL_XY</p></td>
<td><p>0x00000001l</p></td>
<td><p>/ * XY 校准 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_Z</p></td>
<td><p>0x00000002l</p></td>
<td><p>/</em> 校准 Z <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_ISCAL_R</p></td>
<td><p>0x00000004l</p></td>
<td><p>/</em> 校准 R <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_U</p></td>
<td><p>0x00000008l</p></td>
<td><p>/</em> 校准 U <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_ISCAL_V</p></td>
<td><p>0x00000010l</p></td>
<td><p>/</em> 校准 V <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_POV</p></td>
<td><p>0x00000020l</p></td>
<td><p>/</em> 校准 POV * /</p></td>
</tr>
</tbody>
</table>

 

**DwType**成员保留表示的预定义的游戏杆类型的数字。 如果 OEM 校准实用工具设置了此值，它应设置 Mmddk.h 中定义的值范围之外的值。 确切的值是不重要，因为它由标准控件面板重置。

 

 




