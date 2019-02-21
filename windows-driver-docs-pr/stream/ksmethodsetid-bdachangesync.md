---
title: KSMETHODSETID\_BdaChangeSync
description: KSMETHODSETID\_BdaChangeSync
ms.assetid: 260b227d-0d49-4efa-8f8c-4c66886cf9f6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 967b6582f0013b47f77b6014b1152ae8137ea8d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522069"
---
# <a name="ksmethodsetidbdachangesync"></a>KSMETHODSETID\_BdaChangeSync


## <span id="ddk_ksmethodsetid_bdachangesync_ks"></span><span id="DDK_KSMETHODSETID_BDACHANGESYNC_KS"></span>


KSMETHODSETID\_BdaChangeSync 是 BDA 更改同步方法集。 它用于协调对筛选器及其 pin 和节点属性请求的列表。

可采用以下方法：

<span id="KSMETHOD_BDA_START_CHANGES"></span><span id="ksmethod_bda_start_changes"></span>[**KSMETHOD\_BDA\_启动\_更改**](ksmethod-bda-start-changes.md)  
重置更改列表并启动跟踪的一组新的更改。

<span id="KSMETHOD_BDA_CHECK_CHANGES"></span><span id="ksmethod_bda_check_changes"></span>[**KSMETHOD\_BDA\_检查\_更改**](ksmethod-bda-check-changes.md)  
确定是否起作用的请求的更改列表。

<span id="KSMETHOD_BDA_COMMIT_CHANGES"></span><span id="ksmethod_bda_commit_changes"></span>[**KSMETHOD\_BDA\_提交\_更改**](ksmethod-bda-commit-changes.md)  
提交请求的更改的列表。

<span id="KSMETHOD_BDA_GET_CHANGE_STATE"></span><span id="ksmethod_bda_get_change_state"></span>[**KSMETHOD\_BDA\_获取\_更改\_状态**](ksmethod-bda-get-change-state.md)  
确定筛选器的当前更改状态。

### <a name="comments"></a>备注

此方法集是对筛选器实现的。 网络提供程序筛选器可以使用这种方法设置以开始更改的列表，进行更改，然后一次性将它们提交。

 

 





