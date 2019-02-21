---
title: 支持 COPP 的图形适配器输出要求
description: 支持 COPP 的图形适配器输出要求
ms.assetid: e557487d-dba5-4185-9c35-da3185c291f6
keywords:
- 复制保护 WDK COPP，图形适配器输出要求
- 视频复制保护 WDK COPP，图形适配器输出要求
- COPP WDK DirectX VA，图形适配器输出要求
- 受保护的视频 WDK COPP，图形适配器输出要求
- 图形适配器输出要求 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b440160a9fa2af80796c0b0db8b777b3db862ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524445"
---
# <a name="graphics-adapter-output-requirements-to-support-copp"></a>支持 COPP 的图形适配器输出要求


## <span id="ddk_display_adapter_output_requirements_to_support_copp_gg"></span><span id="DDK_DISPLAY_ADAPTER_OUTPUT_REQUIREMENTS_TO_SUPPORT_COPP_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

若要支持 COPP，图形适配器的物理输出连接器必须执行以下任务：

<span id="Protect_key_information"></span><span id="protect_key_information"></span><span id="PROTECT_KEY_INFORMATION"></span>保护密钥的信息  
已认证的输出必须保护已颁发给证书颁发后输出的密钥信息。

<span id="Restrict_unauthorized_components_from_accessing_secure_content"></span><span id="restrict_unauthorized_components_from_accessing_secure_content"></span><span id="RESTRICT_UNAUTHORIZED_COMPONENTS_FROM_ACCESSING_SECURE_CONTENT"></span>限制未经授权的组件访问安全内容  
已认证的输出必须防止未经授权的软件或硬件组件访问通过 COPP 安全通道发送的内容。 已认证的输出应仅允许 COPP 命令，以通过 COPP 安全通道接收的数据进行操作。

<span id="Switch_to_a_failure_mode_if_the_output_fails"></span><span id="switch_to_a_failure_mode_if_the_output_fails"></span><span id="SWITCH_TO_A_FAILURE_MODE_IF_THE_OUTPUT_FAILS"></span>切换到失败模式，如果输出失败  
如果已认证的输出可以不再强制实施在配置时指定的配置配置文件，该输出应停止解密传入的内容，并应将状态消息发送到应用程序。 状态消息应指示配置将无法再执行输出。

 

 





