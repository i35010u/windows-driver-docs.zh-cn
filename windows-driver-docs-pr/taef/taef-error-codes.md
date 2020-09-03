---
title: TAEF 错误代码
description: TAEF 错误代码
ms.assetid: E42AF880-12DA-42b7-AB6D-90011BD7E548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd80111d054a2383f5da1c594a76330a04cdcdb
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403516"
---
# <a name="taef-error-codes"></a>TAEF 错误代码


TAEF 可能会出于各种原因（例如无法连接到计算机来执行跨计算机执行或接收已知测试元数据的无效值）而遇到错误。 出现错误时，TAEF 会显示错误消息，并且通常会显示与该错误关联的 HRESULT 值。 大多数 HRESULT 值都是众所周知的 [系统错误代码](/windows/desktop/Debug/system-error-codes)，但 TAEF 有时会显示自定义错误代码。

## <a name="span-idcustom_taef_hresult_valuesspanspan-idcustom_taef_hresult_valuesspanspan-idcustom_taef_hresult_valuesspancustom-taef-hresult-values"></a><span id="Custom_TAEF_HRESULT_Values"></span><span id="custom_taef_hresult_values"></span><span id="CUSTOM_TAEF_HRESULT_VALUES"></span>自定义 TAEF HRESULT 值


在添加 TAEF 的自定义 HRESULT 值后，将在下表中记录这些值。 目前，只有一个特定于 TAEF 的 HRESULT 值。

| HRESULT                             | 值      | 说明                                                                                                                                                                                                                                    |
|-------------------------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TAEF \_ E \_ 无效的 \_ 测试 \_ 环境 | 0x81A40001 | TAEF 测试通过其元数据请求了无效的测试环境。 影响测试环境的元数据的示例包括 [RunAs](runas.md)、 [ThreadingModel](threading-models.md)和 [ActivationContext](activation-context.md)。 |

 

 

