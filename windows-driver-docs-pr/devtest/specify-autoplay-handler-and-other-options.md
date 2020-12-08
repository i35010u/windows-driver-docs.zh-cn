---
title: 在设备元数据创作向导中指定自动播放处理程序和选项
description: 在设备元数据创作向导中指定自动播放处理程序和选项
keywords:
- 在设备元数据创作向导中指定自动播放处理程序和选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cef3720e9cca446ba9b8550bd3b10aabdc9645de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816911"
---
# <a name="specify-autoplay-handler-and-options-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中指定自动播放处理程序和选项


若要为设备指定选项（包括断开连接状态和自动播放处理程序），请单击 " **选项** " 选项卡。

## <a name="span-iddisconnected_statespanspan-iddisconnected_statespanspan-iddisconnected_statespandisconnected-state"></a><span id="Disconnected_State"></span><span id="disconnected_state"></span><span id="DISCONNECTED_STATE"></span>断开连接状态


若要使设备在断开连接状态下显示，请选择 " **在断开连接状态下显示设备**"。

## <a name="span-idautoplay_handlerspanspan-idautoplay_handlerspanspan-idautoplay_handlerspanautoplay-handler"></a><span id="AutoPlay_Handler"></span><span id="autoplay_handler"></span><span id="AUTOPLAY_HANDLER"></span>自动播放处理程序


当设备连接时，自动播放处理程序允许设备的 UWP 应用程序列在 "自动播放" 选项中。 它不会自动启动应用。

若要为设备定义自动播放处理程序，请从 " **自动播放处理程序**" 下的以下选项中选择 (可选) 。

-   如果不想定义自动播放处理程序，请选择 " **无**"。
-   若要定义自动播放处理程序，请在 **自动播放处理程序** 中填写以下字段：
    -   **包名称**
    -   **发布者**
    -   **应用 ID**
    -   **谓词**
    -   **自动播放类型**
        -   从列表中选择 " **设备** " 或 " **内容**"。
-   若要为桌面应用程序定义自动播放处理程序，请填写 **桌面自动播放处理程序** 下的字段。
    **注意**  不能同时定义自动播放处理程序和桌面自动播放处理程序。

     

 

 





