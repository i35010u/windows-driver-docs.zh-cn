---
title: 预配 API
description: 预配 API
ms.assetid: bcb17631-a13c-416c-ac10-97f6c0d12cb0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6053bed3656bafb0564651075d03e329074808f9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210217"
---
# <a name="provisioning-api"></a>预配 API


通过使用预配 API，你可以为基于 Windows 的计算机设置移动宽带和 Wi-fi 所需的连接配置文件，并且可以配置与移动宽带配置文件关联的成本。 设置信息包含在 XML 文档中，如 [使用元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)中所述。 在购买订阅或更新计算机上的设置信息时，通常会调用此 API。

你还可以随时调用预配 API，以更新提供给 Windows 的信息。 这通常是在移动宽带应用从操作员的服务器检索更新的成本和计划状态时完成的，但也可以在需要更新 Wi-fi 热点网络或移动宽带网络配置时执行此操作。

有关预配 API 的详细信息，请参阅 [**ProvisioningAgent 类**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

 

