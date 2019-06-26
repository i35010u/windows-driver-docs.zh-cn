---
title: 预配 API
description: 预配 API
ms.assetid: bcb17631-a13c-416c-ac10-97f6c0d12cb0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3251e9cacd20d5605fcfee0dee547b88a2c916ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369227"
---
# <a name="provisioning-api"></a>预配 API


通过使用预配 API，你可以预配基于 Windows 的计算机所需的连接配置文件以移动宽带和 Wi-fi，并且可以配置与移动宽带的配置文件相关联的成本。 预配信息包含在 XML 文档，如中所述[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。 订阅购买后或更新的计算机上的设置信息，通常会调用此 API。

此外可以随时更新为 Windows 提供的信息调用预配 API。 这通常是移动宽带应用从操作员的服务器中检索更新的成本和计划状态，但它也可以完成时必须更新的 Wi-fi 热点网络或移动宽带网络配置时。

有关预配 API 的详细信息，请参阅[ **ProvisioningAgent 类**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

 

 






