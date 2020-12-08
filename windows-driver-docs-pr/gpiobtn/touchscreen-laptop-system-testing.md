---
title: 触摸屏笔记本电脑系统测试
description: 本主题介绍适用于触摸计算机的测试系统。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fcc721626f42e9ca5db4b29ec1f7ce1f55f4d869
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791555"
---
# <a name="touchscreen-laptop-system-testing"></a>触摸屏笔记本电脑系统测试


本主题介绍适用于触摸计算机的测试系统。

**屏幕键盘部署 (触摸屏便携式系统仅)**

1.  开启系统并切换到 " **开始** " 屏幕。
2.  执行 [触控键盘部署步骤](indicator-testing.md#touchkbd)。

    *验证*：屏幕键盘不应部署。

3.  将系统 (横向旋转到纵向，并向后) 。

    *验证*：屏幕方向不应更改。

## <a name="span-iddocking_station_testingspanspan-iddocking_station_testingspanspan-iddocking_station_testingspandocking-station-testing"></a><span id="Docking_station_testing"></span><span id="docking_station_testing"></span><span id="DOCKING_STATION_TESTING"></span>扩展坞测试


**将系统以石板模式停靠 (仅限接驳系统的改装)**

1.  如果盖板设备没有键盘) ，则将 GPIO 插接系统 (与连接的 USB 键盘连接在一起。 若要区分停靠和便携式计算机/石板转换，请参阅 [插接与笔记本电脑石板转换](docking-versus-laptop-slate-conversion.md)。 对于改装，请在石板模式下配置系统 (参阅) 的 [盖板/便携式计算机模式转换步骤](indicator-testing.md#conv) 。
2.  以石板模式从系统开始，并将其附加到坞系统。
3.  执行 [触控键盘部署步骤](indicator-testing.md#touchkbd)。

    *验证*：屏幕键盘应部署。

4.  将系统 (横向旋转到纵向，并向后) 。

    *验证*：屏幕方向不应更改。

## <a name="span-idphysical_buttons_testingspanspan-idphysical_buttons_testingspanspan-idphysical_buttons_testingspanphysical-buttons-testing"></a><span id="Physical_buttons_testing"></span><span id="physical_buttons_testing"></span><span id="PHYSICAL_BUTTONS_TESTING"></span>物理按钮测试


系统可向用户公开以下按钮集：

-   电源按钮-必需
-   卷 +/-按钮-必需
-   Windows 按钮-必需
-   旋转锁定按钮-可选

**按钮行为**

-   对于下表中列出的每个按钮和按钮组合，验证是否在所有情况下都出现预期的行为：

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">按钮或组合</th>
    <th align="left">按体验</th>
    <th align="left">按下并保持体验</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left">Windows</td>
    <td align="left">导航到 "开始" 屏幕</td>
    <td align="left">空值</td>
    </tr>
    <tr class="even">
    <td align="left">调高音量</td>
    <td align="left">增加音量</td>
    <td align="left">快速增加音量</td>
    </tr>
    <tr class="odd">
    <td align="left">减小音量</td>
    <td align="left">减小音量</td>
    <td align="left">快速卷减少</td>
    </tr>
    <tr class="even">
    <td align="left">旋转锁定</td>
    <td align="left">旋转锁定切换</td>
    <td align="left">空值</td>
    </tr>
    <tr class="odd">
    <td align="left">强力</td>
    <td align="left">接通电源时待机</td>
    <td align="left"><p>连接的备用系统</p>
    <ul>
    <li>HoldTime 2 &lt; ：输入 CS</li>
    <li>2 &lt; = HoldTime &lt; = 数十：滑动关闭 UX</li>
    <li>HoldTime &gt; 数十：关机</li>
    </ul>
    <p>非连接备用系统</p>
    <ul>
    <li>Holdtime &lt; 4s： enter 睡眠 [optional]</li>
    <li>Holdtime &gt; = 4s:p 下限关闭设备</li>
    </ul></td>
    </tr>
    <tr class="even">
    <td align="left">Windows + 音量向上</td>
    <td align="left">启动或退出讲述人</td>
    <td align="left">空值</td>
    </tr>
    <tr class="odd">
    <td align="left">Windows + 向下音量</td>
    <td align="left">执行屏幕捕获</td>
    <td align="left">空值</td>
    </tr>
    <tr class="even">
    <td align="left">Windows + 电源</td>
    <td align="left">安全注意序列 (显示锁定屏幕) </td>
    <td align="left">空值</td>
    </tr>
    </tbody>
    </table>

     

 

 




