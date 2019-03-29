---
title: DEBUG\_OUTCB\_XXX
description: 调试\_OUTPUTCB\_XXX 常量是输出标记。 输出标记窗体指示之伴随的输出类型的位字段。
ms.date: 11/28/2018
topic_type:
- apiref
api_name:
- DEBUG_OUTCB_TEXT
- DEBUG_OUTCB_DML
- DEBUG_OUTCB_EXPLICIT_FLUSH
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 3aa4ac3c8b0bd599996574a6a02e0fbbe19842ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569080"
---
# <a name="debugoutcbxxx"></a>DEBUG\_OUTCB\_XXX


调试\_OUTCB\_XXX 常量是输出标记。 输出标记窗体指示之伴随的输出类型的位字段。

调试\_OUTCB\_XXX 定义不同类型的输出回调通知可以发送给 Output2。

可能的值包括以下内容。

|Constant|描述|
|-----|-------|
|DEBUG_OUTCB_TEXT|纯文本内容，下面是标志，为掩码参数。|
|DEBUG_OUTCB_DML|调试器标记内容，下面是标志，为掩码参数。|
|DEBUG_OUTCB_EXPLICIT_FLUSH|通知的刷新的显式输出、 标志和自变量均为零。|


<a name="requirements"></a>要求
------------

|||
|-----|-------|
|Header|DbgEng.h （包括 DbgEng.h）|

 

 





