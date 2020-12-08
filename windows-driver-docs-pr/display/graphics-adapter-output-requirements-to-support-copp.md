---
title: 支持 COPP 所要满足的图形适配器输出要求
description: 支持 COPP 所要满足的图形适配器输出要求
keywords:
- 复制保护 WDK COPP，图形适配器输出需求
- 视频复制保护 WDK COPP，图形适配器输出要求
- COPP WDK DirectX VA，图形适配器输出要求
- 受保护的视频 WDK COPP，图形适配器输出需求
- 图形适配器输出要求 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 914b8371eb95eaecad56696bb44025831c000e90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825735"
---
# <a name="graphics-adapter-output-requirements-to-support-copp"></a>支持 COPP 所要满足的图形适配器输出要求


## <span id="ddk_display_adapter_output_requirements_to_support_copp_gg"></span><span id="DDK_DISPLAY_ADAPTER_OUTPUT_REQUIREMENTS_TO_SUPPORT_COPP_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

为了支持 COPP，图形适配器的物理输出连接器必须执行以下任务：

<span id="Protect_key_information"></span><span id="protect_key_information"></span><span id="PROTECT_KEY_INFORMATION"></span>保护密钥信息  
认证的输出必须保护在认证时颁发给输出的密钥信息。

<span id="Restrict_unauthorized_components_from_accessing_secure_content"></span><span id="restrict_unauthorized_components_from_accessing_secure_content"></span><span id="RESTRICT_UNAUTHORIZED_COMPONENTS_FROM_ACCESSING_SECURE_CONTENT"></span>限制未授权的组件访问安全内容  
认证的输出必须防止未经授权的软件或硬件组件访问通过 COPP 安全通道发送的内容。 经过认证的输出应仅允许 COPP 命令对通过 COPP 安全通道接收的数据进行操作。

<span id="Switch_to_a_failure_mode_if_the_output_fails"></span><span id="switch_to_a_failure_mode_if_the_output_fails"></span><span id="SWITCH_TO_A_FAILURE_MODE_IF_THE_OUTPUT_FAILS"></span>如果输出失败，则切换到故障模式  
如果认证的输出不能再强制在配置时指定配置文件，则输出应停止解密传入的内容，并向应用程序发送状态消息。 状态消息应指示输出无法再按配置执行。

 

 





