---
title: Microsoft 驱动程序度量字典附录
description: Microsoft 驱动程序度量字典的辅助资料集合
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: dbaff20d8857aaac03331fd3df5a403fc008e07b
ms.sourcegitcommit: 89b8a43480246dd726e3632aab2db9cf2eb7505d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92254058"
---
# <a name="appendix-for-the-microsoft-driver-measure-dictionary"></a>Microsoft 驱动程序度量字典附录

## <a name="top-microsoft-apps-example"></a>热门 Microsoft 应用示例

|应用程序|应用程序类型|
|----|----|
|Devenv.exe|开发人员工具|
|MS Paint|娱乐|
|Microsoft Skype 应用|Comm & Collab|
|Microsoft Windows 照片|媒体|
|Microsoft Windows 通信应用|工作效率|
|Microsoft 画图|创意|
|Microsoft Solitaire Collection|游戏|
|OneDrive|云存储|
|Windows 组件|Windows 组件|
|Microsoft Edge|浏览器|
|Microsoft Windows DVD 播放器|娱乐|
|Microsoft Zune 视频|媒体|
|Msaccess.exe|开发人员工具|
|Outlook|工作效率|
|Excel|工作效率|
|Internet Explorer|浏览器|
|Msvsmon.exe|开发人员工具|
|我的世界：Windows 10 版本（测试版）|游戏|
|Powershell_Ise.exe|开发人员工具|
|Skype|Comm & Collab|
|Winword.exe|工作效率|
|Lync.exe|Comm & Collab|
|Msosync.exe|云存储|
|Microsoft One Connect|工作效率|
|Windbg.exe|开发人员工具|
|Microsoft Office Onenote|工作效率|
|Microsoft Mahjong|游戏|
|Power Point|工作效率|
|Windbg.exe|开发人员工具|
|Microsoft Office Onenote|工作效率|
|Microsoft Zune 音乐|媒体|
|Microsoft Mahjong|游戏|
|PowerPoint|工作效率|
|我的世界|游戏|
|Microsoft 消息|Comm & Collab|
|Microsoft SkyDrive|云存储|
|Moviemaker.exe|创意|

## <a name="creative-applications-example"></a>创意应用程序示例

|应用程序|
|----|
|MSPaint.exe|
|Photoshop.eve|
|SnagitEditor.exe|
|Adobe Premiere Pro.exe|
|LightRoom.exe|
|AfterFX.eve|
|ClipStudioPaint.exe|
|Audacity.exe|
|SAI.exe|
|FL.exe|

## <a name="display-issues"></a>显示器问题

|应用程序|
|----|
|显示器正在运行但分辨率不佳|
|屏幕闪烁|
|显示器不工作|
|方向异常|
|已打开非最佳显示设置|

## <a name="audio-initialization-benign-failure-codes"></a>音频初始化良性故障代码

### <a name="common-benign-errors"></a>常见良性错误

AEERR_E_EXISTING_DIRECTKS_CLIENT

AEERR_E_EXISTING_EXCLUSIVE_CLIENT

AEERR_E_EXISTING_SHARED_CLIENT

AEERR_E_PIN_LOCKED

AEERR_NO_CONVERTERS_FOUND

AEERR_POLICY_ACCESS_DENIED

AUDCLNT_E_DEVICE_INVALIDATED

### <a name="aeerr_device_in_use-benign-errors"></a>AEERR_DEVICE_IN_USE 良性错误

HResult == AEERR_DEVICE_IN_USE

Platform == Windows.Mobile

OffloadRequested == 1

存在另一个具有相同 AudioClientGuidId 但 OffloadRequested == 0 且 HResult == SUCCESS 的 AudioClientInitialize 事件

### <a name="benign-race-condition-errors"></a>良性争用条件错误

HResult == ERROR_PATH_NOT_FOUND 或 ERROR_NOT_FOUND or ERROR_NOT_CONNECTED

App == Windows 资源管理器或 Windows Shell 体验主机

### <a name="benign-parameter-error"></a>良性参数错误

从应用“videoeditor(plus)”、“screenrecorder”、“neilsenonline”中筛选 ERROR_INVALID_PARAMETER
