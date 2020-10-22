---
title: 注册表设置
description: 注册表设置
ms.assetid: a2536911-0467-4bd0-a63b-55341f0d7567
keywords:
- 操纵杆 WDK HID，注册表设置
- 虚拟游戏杆驱动程序 WDK HID，注册表设置
- VJoyD WDK HID，注册表设置
- 注册表 WDK 游戏杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417ae386819fb415c34740c4c8ff9a65849fe280
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356009"
---
# <a name="registry-settings"></a>注册表设置

操纵杆接口使用注册表存储配置、校准和用户首选项信息。 它还用于存储校准程序的自定义文本。 可以通过注册表自定义 Windows 95/98/Me 操纵杆校准程序，以便在特定于操纵杆的校准期间向用户提供说明。

值分为五组：

由 OEM 提供并从 INF 文件中安装的原始数据 (前面所述) 。

## <a name="user-values"></a>用户值

当前注册表设置有两个部分：要存储的值，它是标准轮询的替代，以及存储功能、校准值和微型驱动程序数据的键。

用于轮询没有关联微型驱动程序的设备以替换标准轮询的微型驱动程序可以在名为 REGSTR VAL JOYCALLOUT 的项中定义 \_ \_ 。 此功能是 DirectX 3.0 的新增功能。 当用户从列表中选择一个新的全局驱动程序时，将从 "高级设置" 页设置这些值，其中包含具有 "乐趣 \_ HWS ISGAMEPORTDRIVER" 标志集的所有微型驱动程序 \_ 。

其余设置将存储在 REGSTR \_ key \_ JOYCURR 键下。 当设备首次配置为特定操纵杆 ID 时，控制面板会将 REGSTR PATH JOYOEM 下相关 OEM 密钥中的值复制 \_ \_ 到 REGSTR \_ key \_ JOYCURR 项。 此项下的每个键值名称包含游戏杆 ID 作为名称的一部分，因此每个操纵杆都有其自己的设置。 REGSTR \_ VAL \_ JOYOEMNAME 值将复制到相关的 REGSTR \_ VAL \_ JOYNOEMNAME 中，如果存在，则将 REGSTR \_ VAL \_ JOYOEMCALLOUT 值复制到 REGSTR \_ val \_ JOYNOEMCALLOUT。 REGSTR \_ VAL \_ JOYOEMDATA 值用作 REGSTR val JOYNCONFIG 值的前两个双字 \_ ，其中的 \_ 所有值在展开) 时 (定义，如下所示：

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

使用设置是以下值的组合：

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
<td><p>/* 用方向舵配置的操纵杆 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_US_PRESENT</p></td>
<td><p>0x00000002l</p></td>
<td><p>/</em> 游戏杆是否确实会出现？ <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_US_ISOEM</p></td>
<td><p>0x00000004l</p></td>
<td><p>/</em> 游戏杆为 OEM 定义的类型 <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_US_RESERVED</p></td>
<td><p>0x80000000l</p></td>
<td><p>/</em> 保留 */</p></td>
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
<td><p>/* XY <em>/</p></td>
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
<td><p>/</em> 校准了 U <em>/</p></td>
</tr>
<tr class="odd">
<td><p>JOY_ISCAL_V</p></td>
<td><p>0x00000010l</p></td>
<td><p>/</em> 校准 V <em>/</p></td>
</tr>
<tr class="even">
<td><p>JOY_ISCAL_POV</p></td>
<td><p>0x00000020l</p></td>
<td><p>/</em> 校准了 POV */</p></td>
</tr>
</tbody>
</table>

 **DwType**成员包含表示预定义游戏杆类型的数字。 如果 OEM 校准实用程序设置了此值，则应在 Mmddk 中定义的值范围之外设置值。 确切的值并不重要，因为它是由标准控制面板重置的。

## <a name="current-settings"></a>当前设置

在安装过程中，将从 INF 文件设置这些注册表设置，如 [创建 Inf 文件](creating-an-inf-file.md)和启动时在设备枚举过程中所述。

## <a name="saved-settings"></a>保存的设置

保存当前操纵杆设置后， \_ \_ 保存在 REGSTR key JOYCURR 项下的 REGSTR VAL \_ JOYNCONFIG \_ 也会写入 \_ \_ 子项中与 OEM 定义的设置相同的名称下的 REGSTR key JOYSETTINGS 键下， (非 OEM 设置保存在子项 "predef" 中，并) 的类型编号。 当播放操纵杆时，保存的设置将保留，以便在游戏杆恢复时，保存的设置将返回当前设置。 这些注册表值仅用于 "控制面板"。

## <a name="driver-settings"></a>驱动程序设置

名为 REGSTR VAL JOYUSERVALUES 的单个值 \_ \_ 存储如下所述的结构。 此结构指定当应用程序请求对数据进行缩放、居中或定义了死区时，VJoyD 应如何处理数据。

```cpp
struct {
    /* value at which to time-out internal joystick polling */
    DWORD   dwTimeOut;

    /* range of values app wants returned for axes */
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
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpCenter;
    } jrvRanges;

    /* area around center to be considered as "dead". specified as */
    /* a percentage (0-100). Only X & Y handled by system driver */
    struct {
        DWORD    dwX;
        DWORD    dwY;
        DWORD    dwZ;
        DWORD    dwR;
        DWORD    dwU;
        DWORD    dwV;
    } jpDeadZone;
}
```

用户值、当前设置和已保存的设置都存储在注册表中的 "当前" 游戏杆驱动程序的路径下。 安装了驱动程序的每个操纵杆设备在路径 REGSTR 路径 JOYCONFIG 下都有一个名为 \_ \_ Msjstick. winspool.drv xxxx 的键 &lt; *xxxx* &gt; ，其中*xxxx*是用于使密钥名称唯一的四位数字。 该数字与已安装的多媒体 (声音、视频和游戏控制器) 驱动程序的数目相关。 在启动时，Msjstick 将初始化为每个游戏控制器驱动程序的配置。 由于它每次只能处理一个配置，因此，每个配置都将替换最后一个，而 "当前" 驱动程序则是最后一个要初始化的驱动程序。 这意味着，在安装新的驱动程序时，用户可能会丢失所有当前设置，并且无法通过假设这些注册表值的路径始终相同来构造微型驱动程序。
