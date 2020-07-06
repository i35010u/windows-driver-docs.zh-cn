---
title: 调试 \_ OUTCB \_ XXX
description: DEBUG \_ OUTPUTCB \_ XXX 常量是输出标志。 输出标志构成一个位域，该字段指示附带输出的输出类型。
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
ms.openlocfilehash: ce23bc0a751c52eab4eaf65fb84c9965330c7403
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968020"
---
# <a name="debug_outcb_xxx"></a>调试 \_ OUTCB \_ XXX


DEBUG \_ OUTCB \_ XXX 常量是输出标志。 输出标志构成一个位域，该字段指示附带输出的输出类型。

DEBUG \_ OUTCB \_ XXX 定义可发送到输出2的不同类型的输出回调通知。

可能的值包括以下各项。

|返回的常量|描述|
|-----|-------|
|DEBUG_OUTCB_TEXT|纯文本内容，标志为，参数为 mask。|
|DEBUG_OUTCB_DML|调试器标记内容，标志为，参数为 mask。|
|DEBUG_OUTCB_EXPLICIT_FLUSH|显式输出刷新、标志和自变量的通知为零。|


<a name="requirements"></a>要求
------------

**标头**： DbgEng （包括 DbgEng）


 

 





