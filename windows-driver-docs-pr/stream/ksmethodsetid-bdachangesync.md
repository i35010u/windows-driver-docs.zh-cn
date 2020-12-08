---
title: KSMETHODSETID \_ BdaChangeSync
description: KSMETHODSETID \_ BdaChangeSync
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19c175d42f9360e87e47d5f24e52000b0c152acd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819969"
---
# <a name="ksmethodsetid_bdachangesync"></a>KSMETHODSETID \_ BdaChangeSync


## <span id="ddk_ksmethodsetid_bdachangesync_ks"></span><span id="DDK_KSMETHODSETID_BDACHANGESYNC_KS"></span>


KSMETHODSETID \_ BdaChangeSync 为 BDA 更改同步方法集。 它用于协调筛选器及其引脚和节点上的属性请求列表。

有以下方法可用：

<span id="KSMETHOD_BDA_START_CHANGES"></span><span id="ksmethod_bda_start_changes"></span>[**KSMETHOD \_ BDA \_ 开始 \_ 更改**](ksmethod-bda-start-changes.md)  
重置更改列表，并开始跟踪一组新的更改。

<span id="KSMETHOD_BDA_CHECK_CHANGES"></span><span id="ksmethod_bda_check_changes"></span>[**KSMETHOD \_ BDA \_ 检查 \_ 更改**](ksmethod-bda-check-changes.md)  
确定请求的更改列表是否有效。

<span id="KSMETHOD_BDA_COMMIT_CHANGES"></span><span id="ksmethod_bda_commit_changes"></span>[**KSMETHOD \_ BDA \_ 提交 \_ 更改**](ksmethod-bda-commit-changes.md)  
提交请求的更改的列表。

<span id="KSMETHOD_BDA_GET_CHANGE_STATE"></span><span id="ksmethod_bda_get_change_state"></span>[**KSMETHOD \_ BDA \_ 获取 \_ 更改 \_ 状态**](ksmethod-bda-get-change-state.md)  
确定筛选器的当前更改状态。

### <a name="comments"></a>注释

此方法集是在筛选器上实现的。 网络提供程序筛选器可以使用此方法设置来开始更改列表，进行更改，然后一次性提交这些更改。

 

 





