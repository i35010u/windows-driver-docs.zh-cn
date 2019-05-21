---
title: WIA_IPS_BLANK_PAGES_SENSITIVITY
description: WIA_IPS_BLANK_PAGES_SENSITIVITY 属性用于将空白页检测触发器更改为较低或更高版本的设备支持的最低和最高敏感度介于。
keywords:
- WIA_IPS_BLANK_PAGES_SENSITIVITY 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BLANK_PAGES_SENSITIVITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3d4c904d592713d7f398ef7c7c4ce458d70f9bc6
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958681"
---
# <a name="wiaipsblankpagessensitivity"></a>WIA\_IPS\_空白\_页面\_敏感度

**WIA\_IPS\_空白\_页\_敏感度**属性用于将空白页检测触发器更改为较低或更高版本的最低和最高敏感度介于支持的设备。

WIA 微型驱动程序可以在内部为每个使用单独的敏感度值[ **WIA\_IPA\_数据\_类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)并[ **WIA\_IPA\_深度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)支持颜色模式组合。

此属性是初始化和维护的 WIA 微型驱动程序。

属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读写

## <a name="remarks"></a>备注

此属性是可选的仅对送纸器项有效 (WIA\_类别\_送纸器)，仅当[ **WIA\_IP\_空白\_页**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-blank-pages)上至少有一个比另一个值支持**WIA\_空白\_页\_检测\_禁用**。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef.h （包括 Wiadef.h） |
