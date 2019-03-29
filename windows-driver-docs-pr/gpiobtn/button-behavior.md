---
title: 按钮行为
description: 本主题介绍的硬件按钮的预期的行为。
ms.assetid: 057A4F21-3514-4CCA-BCE2-279E8228B5A9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: db3152b8a63d774b5220ab35b66265586f84f1a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562052"
---
# <a name="button-behavior"></a>按钮行为


本主题介绍的硬件按钮的预期的行为。

## <a name="span-idrequiredandoptionalbuttonsinwindows10spanspan-idrequiredandoptionalbuttonsinwindows10spanspan-idrequiredandoptionalbuttonsinwindows10spanrequired-and-optional-buttons-in-windows10"></a><span id="Required_and_optional__buttons_in_Windows_10"></span><span id="required_and_optional__buttons_in_windows_10"></span><span id="REQUIRED_AND_OPTIONAL__BUTTONS_IN_WINDOWS_10"></span>Windows 10 中的必需和可选按钮


<table>
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">操作系统/设备</td>
<td align="left">电源</td>
<td align="left">音量增大 / 减小音量</td>
<td align="left">开始时间</td>
<td align="left">返回/搜索</td>
<td align="left">相机</td>
<td align="left">旋转锁定</td>
</tr>
<tr class="even">
<td align="left">Windows 10 移动版</td>
<td align="left">必需</td>
<td align="left">必需</td>
<td align="left"><p>所需的使用 WVGA 显示的手机</p>
<p>对于所有其他设备来说为可选</p></td>
<td align="left"><p>所需的使用 WVGA 显示的手机</p>
<p>对于所有其他设备来说为可选</p></td>
<td align="left">可选</td>
<td align="left">不支持</td>
</tr>
<tr class="odd">
<td align="left">（主页、 专业版、 企业版和教育版） 的桌面版本的 Windows 10 平板电脑 /</td>
<td align="left">必需</td>
<td align="left">必需</td>
<td align="left">可选</td>
<td align="left">不支持</td>
<td align="left">不支持</td>
<td align="left">可选</td>
</tr>
<tr class="even">
<td align="left">面向桌面版本的 Windows 10 / 其他设备</td>
<td align="left">必需</td>
<td align="left">使用可拆卸键盘的设备所必需。 对于所有其他设备可选。</td>
<td align="left">可选</td>
<td align="left">不支持</td>
<td align="left">不支持</td>
<td align="left">可选</td>
</tr>
</tbody>
</table>

 

有关按钮要求的详细信息：

-   Windows 10 移动版，请参阅中的部分 2.6[最低硬件要求](https://msdn.microsoft.com/library/windows/hardware/dn915086.aspx)。
-   对于桌面版本的 Windows 10，请参阅中的部分 3.6[最低硬件要求](https://msdn.microsoft.com/library/windows/hardware/dn915086.aspx)。

## <a name="span-idbuttonbehaviorinwindows10spanspan-idbuttonbehaviorinwindows10spanspan-idbuttonbehaviorinwindows10spanbutton-behavior-in-windows10"></a><span id="Button_behavior_in_Windows_10"></span><span id="button_behavior_in_windows_10"></span><span id="BUTTON_BEHAVIOR_IN_WINDOWS_10"></span>Windows 10 中的按钮行为


### <a name="span-idsinglebuttonbehaviorinwindows10spanspan-idsinglebuttonbehaviorinwindows10spanspan-idsinglebuttonbehaviorinwindows10spansingle-button-behavior-in-windows10"></a><span id="Single_button_behavior_in_Windows_10"></span><span id="single_button_behavior_in_windows_10"></span><span id="SINGLE_BUTTON_BEHAVIOR_IN_WINDOWS_10"></span>Windows 10 中的单个按钮行为

面向 Windows 10 移动 Power 按桌面版本和版本切换开/关切换开/关按按钮 Windows 10 并按住启动关闭窗帘启动关闭窗帘长按下并保持硬关机硬件重置搜索按和不受支持的版本启动 （在启用了市场） 的 Cortana / 搜索按下并保持不支持启动 Cortana 或使用语音音量增大按搜索和发布增量卷增量卷按，然后保存自动重复音量增量自动重复卷增加按减小音量和发布递减量递减卷按和保存自动重复卷递减自动重复卷递减返回按和上一步应用程序页 / 关闭应用上一步应用程序页 / 关闭应用按发布并保存 UI 启动的启动任务切换器启动切换器切换开始屏幕显示开始屏幕旋转锁不支持不受支持 （没有用户界面选项） 照相机焦点启动相机应用程序已处理的相机应用程序 （关注） 相机快门已处理的相机应用程序启动相机应用程序 / 拍摄图片
 

### <a name="span-idbuttoncombinationbehaviorinwindows10spanspan-idbuttoncombinationbehaviorinwindows10spanspan-idbuttoncombinationbehaviorinwindows10spanbutton-combination-behavior-in-windows10"></a><span id="Button_combination_behavior_in_Windows_10"></span><span id="button_combination_behavior_in_windows_10"></span><span id="BUTTON_COMBINATION_BEHAVIOR_IN_WINDOWS_10"></span>Windows 10 中的按钮组合行为

如前所述，在 Windows 10 中某些按钮组合应用于[Windows 10 按钮体系结构](https://msdn.microsoft.com/library/windows/hardware/dn957423%28v=vs.85%29.aspx)或 Windows 8.1 按钮体系结构。 Windows 10 中的所有其他按钮组合应用于任一按钮体系结构。 建议来描述使用 Windows 10 体系结构的硬件按钮。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">按钮组合</td>
<td align="left">Windows 10 桌面版</td>
<td align="left">Windows 10 移动版</td>
</tr>
<tr class="even">
<td align="left">开始时间 + 调高音量</td>
<td align="left">屏幕上切换讲述人</td>
<td align="left">屏幕上切换讲述人 （前提是相应的轻松访问设置已启用）</td>
</tr>
<tr class="odd">
<td align="left">开始时间 + 减小音量</td>
<td align="left">拍摄的屏幕快照</td>
<td align="left">不支持</td>
</tr>
<tr class="even">
<td align="left">开始时间 + 电源</td>
<td align="left">（仅当使用 Windows 8.1 按钮体系结构） Ctrl + Alt + Del</td>
<td align="left">不支持</td>
</tr>
<tr class="odd">
<td align="left">Power + 调高音量</td>
<td align="left">（仅当使用 Windows 10 按钮体系结构） 拍摄的屏幕快照</td>
<td align="left">拍摄的屏幕快照</td>
</tr>
<tr class="even">
<td align="left">Power + 向下的卷</td>
<td align="left">（仅当使用 Windows 10 按钮体系结构） Ctrl + Alt + Del</td>
<td align="left"><p>启动 Windows 反馈应用</p>
<p>硬件重置 （在 10 秒）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idbuttonbehaviorinwindows81spanspan-idbuttonbehaviorinwindows81spanbutton-behavior-in-windows-81"></a><span id="button_behavior_in_windows_8.1"></span><span id="BUTTON_BEHAVIOR_IN_WINDOWS_8.1"></span>在 Windows 8.1 中的按钮行为


### <a name="span-idsinglebuttonbehaviorinwindows81spanspan-idsinglebuttonbehaviorinwindows81spanspan-idsinglebuttonbehaviorinwindows81spansingle-button-behavior-in-windows-81"></a><span id="Single_button_behavior_in_Windows_8.1"></span><span id="single_button_behavior_in_windows_8.1"></span><span id="SINGLE_BUTTON_BEHAVIOR_IN_WINDOWS_8.1"></span>在 Windows 8.1 中的单个按钮行为

Windows 8.1 的 Windows 8.1 Phone Power 按按钮操作和发布切换开/关切换开/关按按住启动关闭窗帘启动关闭窗帘长按，保存硬关机硬件重置搜索按和版本不支持启动 Cortana 按和保留不支持使用语音音量增大按启动 Cortana 和发布增量卷增量卷按和保存自动重复音量增量自动重复卷增加音量降低按和发布递减量递减卷按并保存自动重复卷递减自动重复卷递减回不支持不支持启动切换启动屏幕切换启动屏幕旋转锁版本：锁定旋转锁旋转照相机焦点不支持不适用的相机快门不支持不适用
 

### <a name="span-idbuttoncombinationbehaviorinwindows81spanspan-idbuttoncombinationbehaviorinwindows81spanspan-idbuttoncombinationbehaviorinwindows81spanbutton-combination-behavior-in-windows-81"></a><span id="Button_combination_behavior_in_Windows_8.1"></span><span id="button_combination_behavior_in_windows_8.1"></span><span id="BUTTON_COMBINATION_BEHAVIOR_IN_WINDOWS_8.1"></span>在 Windows 8.1 中的按钮组合行为

|                     |                           |                               |
|---------------------|---------------------------|-------------------------------|
| 按钮组合  | Windows 8.1               | Windows 8.1 Phone             |
| 开始时间 + 调高音量   | 屏幕上切换讲述人 | 不支持                 |
| 开始时间 + 减小音量 | 拍摄的屏幕快照           | 不支持                 |
| 开始时间 + 电源       | Ctrl+Alt+Del              | 不支持                 |
| Power + 调高音量   | 不支持             | 拍摄的屏幕快照               |
| Power + 向下的卷 | 不支持             | 硬件重置 （在 10 秒） |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[Windows 10 按钮体系结构](https://msdn.microsoft.com/library/windows/hardware/dn957423%28v=vs.85%29.aspx)  
[最低硬件要求](https://msdn.microsoft.com/library/windows/hardware/dn915086.aspx)  



