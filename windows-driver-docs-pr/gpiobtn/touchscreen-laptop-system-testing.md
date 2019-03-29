---
title: 触摸屏笔记本电脑系统测试
description: 本主题介绍针对触摸屏便携式计算机系统测试。
ms.assetid: 0DD7865F-C31C-48AD-8775-4AC1E469176F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf95ec0a0826da32f61aac4cfce28a67a25cc5b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563150"
---
# <a name="touchscreen-laptop-system-testing"></a>触摸屏笔记本电脑系统测试


本主题介绍针对触摸屏便携式计算机系统测试。

**屏幕键盘部署 （仅限触摸屏便携式计算机系统）**

1.  系统接通电源后，转到**启动**屏幕。
2.  执行[触摸键盘部署步骤](indicator-testing.md#touchkbd)。

    *验证*:不应部署屏幕键盘。

3.  旋转系统 （横向与纵向）。

    *验证*:不应更改屏幕方向。

## <a name="span-iddockingstationtestingspanspan-iddockingstationtestingspanspan-iddockingstationtestingspandocking-station-testing"></a><span id="Docking_station_testing"></span><span id="docking_station_testing"></span><span id="DOCKING_STATION_TESTING"></span>停靠工作站测试


**停靠盖板模式 （仅限于停靠系统与双用型） 中的系统**

1.  有 GPIO 停靠 （与 USB 键盘附加平板设备是否没有键盘） 可用的系统。 停靠和便携式计算机/盖板转换之间的区别，请参阅[停靠与便携式计算机盖板转换](docking-versus-laptop-slate-conversion.md)。 对于双用型，在平板式模式下配置系统 (请参阅[盖板/便携式计算机模式转换步骤](indicator-testing.md#conv))。
2.  在静态模式下启动系统并将其附加到停靠的系统。
3.  执行[触摸键盘部署步骤](indicator-testing.md#touchkbd)。

    *验证*:应该部署屏幕键盘。

4.  旋转系统 （横向与纵向）。

    *验证*:不应更改屏幕方向。

## <a name="span-idphysicalbuttonstestingspanspan-idphysicalbuttonstestingspanspan-idphysicalbuttonstestingspanphysical-buttons-testing"></a><span id="Physical_buttons_testing"></span><span id="physical_buttons_testing"></span><span id="PHYSICAL_BUTTONS_TESTING"></span>测试的物理按钮


系统可以公开给用户的按钮的以下设置：

-   电源按钮-所需
-   卷 + /-按钮 – 必需
-   Windows 按钮-将所需
-   旋转锁按钮-可选

**按钮行为**

-   对于每个按钮和下表中列出的按钮组合，验证在所有情况下会发生的预期的行为：

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
    <td align="left">导航到开始屏幕</td>
    <td align="left">不可用</td>
    </tr>
    <tr class="even">
    <td align="left">调高音量</td>
    <td align="left">增大音量</td>
    <td align="left">快速的卷的大小</td>
    </tr>
    <tr class="odd">
    <td align="left">减小音量</td>
    <td align="left">减小音量</td>
    <td align="left">快速卷减少</td>
    </tr>
    <tr class="even">
    <td align="left">旋转锁</td>
    <td align="left">旋转锁切换</td>
    <td align="left">不可用</td>
    </tr>
    <tr class="odd">
    <td align="left">电源</td>
    <td align="left">打开连接待机电源</td>
    <td align="left"><p>连接待机系统</p>
    <ul>
    <li>HoldTime&lt;2： 输入 CS</li>
    <li>2&lt;= HoldTime&lt;= 10 秒： 关闭用户体验的幻灯片</li>
    <li>HoldTime&gt;10 秒： 打开和关闭电源</li>
    </ul>
    <p>非连接待机系统</p>
    <ul>
    <li>Holdtime&lt; 4 秒： 进入睡眠状态 [可选]</li>
    <li>Holdtime&gt;= 4 秒： 打开和关闭设备电源</li>
    </ul></td>
    </tr>
    <tr class="even">
    <td align="left">Windows + 调高音量</td>
    <td align="left">启动或退出讲述人</td>
    <td align="left">不可用</td>
    </tr>
    <tr class="odd">
    <td align="left">Windows + 向下的卷</td>
    <td align="left">执行屏幕捕获</td>
    <td align="left">不可用</td>
    </tr>
    <tr class="even">
    <td align="left">Windows + 电源</td>
    <td align="left">安全注意序列 （显示锁定屏幕）</td>
    <td align="left">不可用</td>
    </tr>
    </tbody>
    </table>

     

 

 




