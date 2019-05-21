---
title: WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS
description: WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS 属性描述要始终打印页计数器的最小位数。
keywords:
- WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9f5f675abdfbaf8a044c6a875fae7d34de74dda
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958679"
---
# <a name="wiaipsprinterendorsercounterdigits"></a>WIA\_IPS\_打印机\_印记签署器\_计数器\_数字

**WIA\_IPS\_打印机\_印记签署器\_计数器\_数字**属性描述要始终打印页计数器的最小位数。 其余的空数字，如果有，必须使用填充指定的填充字符[ **WIA\_IPS\_打印机\_印记签署器\_填充**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-printer-endorser-padding)属性，如果受支持，或为零 (0)，否则为使用。

此属性是初始化和维护的 WIA 微型驱动程序。

属性类型：VT\_UI4

有效值：WIA\_PROP\_NONE

访问权限：只读

## <a name="remarks"></a>备注

此属性是可选的印刷器/印记签署器对有效项的支持[ **WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-printer-endorser-valid-format-specifiers)具有属性**WIA\_打印\_页\_计数**值。 实现时，属性值必须严格大于零 (0)。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef.h （包括 Wiadef.h） |
